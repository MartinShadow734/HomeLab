# HomeLab

Hands-on IT infrastructure, virtualization, networking, and cybersecurity projects built on a compact 10-inch rack with Proxmox and Linux.

I'm Martin Capula, an IT Support Technician working toward NOC and Security Analyst roles. I hold CompTIA Security+ and ISC2 CC and I'm studying for the CCNA. This lab is where I practice the skills those roles need, and every project here is documented the way I would document work on the job: what I built, why, what broke, how I fixed it, and how I verified it.

> **Status:** Build in progress. Projects are marked honestly as Complete, In progress, or Planned.

## Lab at a glance

| Component | Details |
|---|---|
| Hypervisor | Lenovo ThinkCentre M920q Tiny, Intel i5-8500T (6 cores), running Proxmox VE |
| Switch | HPE Aruba Instant On 1830 8G, Layer 2 smart-managed (VLANs, port mirroring, LACP, 802.1X) |
| Rack | DeskPi RackMate T1 Plus, 10-inch 8U, with keystone patch panel |
| Network | Lab sits behind the household router and stays isolated from it. OPNsense will route and firewall the lab VLANs |
| Remote access | SSH and Tailscale |

Full parts list and build notes: [hardware.md](hardware.md)

## Architecture

<!-- After the audit, add the diagram: ![Lab network diagram](diagrams/network-overview.png) -->

*Diagram coming after the baseline audit. Planned design: Proxmox management stays on the home network, and lab VLANs for management, servers, clients, and an isolated attack network sit behind an OPNsense virtual firewall.*

## Projects

| # | Project | Skills | Status |
|---|---|---|---|
| 01 | [Proxmox Virtualization](projects/01-proxmox-virtualization/) | Type 1 hypervisor, VM lifecycle, VM migration, remote administration | In progress |
| 02 | Backups and Disaster Recovery | Scheduled backups, retention, restore testing, RPO and RTO | Planned |
| 03 | Physical Build and Switch Hardening | Structured cabling, port mapping, switch first-boot security | Planned |
| 04 | VLAN Segmentation | 802.1Q, trunk and access ports, subnetting | Planned |
| 05 | OPNsense Firewall | Stateful firewalling, NAT, inter-VLAN routing, rule design | Planned |
| 06 | Linux Hardening and SSH Security | Key-based auth, hardware security keys, least privilege, patching | Planned |
| 07 | Monitoring | Prometheus, Grafana, alerting | Planned |
| 08 | Active Directory | AD DS, DNS, DHCP, Group Policy | Planned |
| 09 | SIEM with Wazuh | Log collection, detection rules, alert triage | Planned |
| 10 | Vulnerability Management | Scanning, CVSS prioritization, remediation | Planned |
| 11 | IDS and Traffic Analysis | Suricata, Wireshark, port mirroring | Planned |
| 12 | Incident Response Exercise | NIST IR lifecycle, detection, containment, recovery | Planned |
| 13 | Automation | Ansible, configuration as code | Planned |

## How each project is documented

Every write-up follows the same structure ([template](templates/PROJECT-TEMPLATE.md)):

1. Objective and the problem being solved
2. Architecture and tools
3. Implementation steps and the reasoning behind them
4. Problems encountered and how I troubleshot them
5. Validation and evidence
6. Lessons learned and next improvements

## Security note

This repository is public, so all screenshots, configs, and diagrams are sanitized before publishing. Passwords, keys, public IPs, device identifiers, and location data are never included. See the [redaction checklist](docs/REDACTION-CHECKLIST.md).

## Connect

<!-- Add your LinkedIn URL below, then delete this comment -->
- LinkedIn: *link coming soon*
- Other projects: [Healthcare Patient Flow Dashboard](https://github.com/MartinShadow734/healthcare-patient-flow-dashboard)
