# Project 03: Infrastructure Monitoring with Prometheus and Grafana

**Status:** Complete  
**Date completed:** November 2026  
**Skills:** Observability, metrics collection, time-series monitoring, Linux containers (LXC), infrastructure-as-code, dashboarding  
**Relevant to:** NOC Technician, SOC Analyst, Site Reliability Engineer, Systems Administrator

## Objective

Build visibility into the lab's health before scaling it up. A NOC technician or site reliability engineer spends most of their day in dashboards and alerts, so collecting metrics, storing them, and surfacing problems on a single screen is a core operational skill. The goal here was a working observability stack that shows CPU, memory, disk, and network health at a glance and keeps running on its own.

## Architecture

| Component | Role |
|---|---|
| Proxmox VE host | The system being monitored |
| node_exporter | Agent on the host that exposes system metrics |
| Dedicated LXC container (Debian, unprivileged) | Isolates the monitoring stack from other workloads |
| Prometheus | Scrapes and stores time-series metrics |
| Grafana | Dashboards and visualization on top of Prometheus |

## Tools and technologies

- **node_exporter:** exposes host metrics (CPU, memory, disk, network, load) for collection
- **Prometheus:** time-series database that scrapes metrics on a schedule and stores the history
- **Grafana:** visualization layer that queries Prometheus and renders dashboards
- **LXC (unprivileged container):** lightweight isolation for the monitoring services
- **Provisioning (infrastructure-as-code):** Grafana's data source and dashboard defined in configuration files instead of clicked by hand

## Work completed

- Deployed node_exporter on the Proxmox host to expose system metrics
- Created a dedicated, unprivileged Linux container so the monitoring stack is isolated from other workloads
- Installed and configured Prometheus to scrape the host on a schedule and retain history
- Installed Grafana, connected it to Prometheus, and loaded a full host dashboard (CPU, memory, disk, network, load)
- Configured Grafana entirely through provisioning files so the setup is repeatable rather than hand-clicked
- Set every service to start automatically on reboot

## Implementation

### Isolating the stack in its own container

Rather than installing the monitoring tools directly on the host, I built them inside a dedicated, unprivileged Linux container. This keeps the stack separate from other workloads, limits what a compromise of those services could reach, and makes the whole thing easy to move or rebuild. Unprivileged containers are the safer default because the container's root user is not the host's root user.

### Metrics pipeline: exporter to Prometheus to Grafana

The data flows one direction. node_exporter runs on the host and publishes its metrics. Prometheus reaches out on a fixed interval, pulls those metrics, and stores them with timestamps, so there is history to look back on rather than only a live snapshot. Grafana sits on top, queries Prometheus, and turns the numbers into readable dashboards. I verified the pipeline end to end by confirming Prometheus reported every scrape target as healthy before building anything on it.

### Configuration as code

Instead of clicking through Grafana's web interface to connect the data source and import a dashboard, I defined both in configuration files that Grafana reads on startup. This is the infrastructure-as-code approach: the setup is version-controllable, repeatable, and documented by the files themselves. Rebuilding the stack means re-applying the files, not remembering a sequence of clicks.

### Validation

- Confirmed node_exporter was active and publishing metrics on the host
- Confirmed Prometheus reported all scrape targets as healthy
- Confirmed Grafana loaded the provisioned data source and dashboard and rendered live host metrics
- Rebooted and confirmed every service came back automatically

## Key outcomes

- A single pane of glass for host health, the foundation every later monitoring and detection project builds on
- A repeatable, code-defined setup rather than a hand-built one
- Hands-on practice with the exact Prometheus and Grafana stack used across NOC, SRE, and SOC teams

## What's next

- Add an alert (low disk space or host down) with a notification
- Extend monitoring to additional nodes and the firewall as that hardware is deployed
- Feed these metrics alongside security logs once a SIEM is in place

*(Specific addresses, hostnames, and identifiers are kept in private records, not this public writeup.)*
