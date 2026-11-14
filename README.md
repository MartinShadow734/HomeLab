# HomeLab | Infrastructure & Security Portfolio

Hands-on projects in **virtualization, Linux administration, networking, and cybersecurity**, built to demonstrate practical IT and troubleshooting skills.

I'm Martin Capula. I work in IT support and am developing toward NOC and security analyst roles. I hold **CompTIA Security+**, **CompTIA A+**, and **ISC2 CC**, and I'm studying for the **CCNA**.

## Start here: Featured project

### [01 · Proxmox Virtualization and Two-Node Cluster](projects/01-proxmox-virtualization/README.md)
**Operational; backup restore testing pending** | Proxmox VE · Two-node cluster · Ubuntu Server · SSH · Tailscale · VirtualBox migration

**Relevant to:** Systems Administrator, NOC Technician, IT Support

**Challenge:** Run and manage multiple server workloads across a compact two-node Proxmox cluster with asymmetric capacity, and diagnose it when it breaks.

**What I've done:** Installed Proxmox VE on two Lenovo M920q Tiny nodes, joined them into a cluster, migrated a workload from VirtualBox, configured remote administration, and diagnosed a cluster quorum loss after a rack power outage.

**What this demonstrates:** Hypervisor administration, two-node cluster operation, VM migration, Linux CLI, remote connectivity, and evidence-driven troubleshooting of a real incident.

**Evidence still being prepared:** Sanitized architecture diagram, a timed backup-and-restore test, and a dashboard capture of a host-down alert.

[Explore the project →](projects/01-proxmox-virtualization/README.md)

### [02 · Linux Hardening and Security Auditing](projects/02-linux-hardening/README.md)

Hardened two Linux systems with a repeatable measure-fix-verify process using Lynis, fail2ban, and rootkit detection, raising each system's hardening score and documenting the method and lessons learned. **Relevant to:** Security Analyst, NOC, Sysadmin.

[Explore the project →](projects/02-linux-hardening/README.md)

### [03 · Infrastructure Monitoring with Prometheus and Grafana](projects/03-monitoring/README.md)

**Operational; alerting and hardening pending** | Built an isolated, code-provisioned observability stack (node_exporter, Prometheus, Grafana) on Proxmox, with a live host dashboard for CPU, memory, disk, and network that survives reboots. **Relevant to:** NOC Technician, SOC Analyst, SRE.

[Explore the project →](projects/03-monitoring/README.md)

## Skills at a glance

| Area | Hands-on work |
|---|---|
| Virtualization | Proxmox VE, VM deployment and migration |
| Linux | Ubuntu Server, headless administration, SSH |
| Remote access | Tailscale, SSH connectivity troubleshooting |
| Infrastructure planning | Compact rack, hardware selection, planned network segmentation |
| Monitoring & observability | Prometheus, Grafana, node_exporter, infrastructure-as-code provisioning |
| Documentation | Architecture decisions, implementation notes, validation plans |

## What's next

These projects are **planned, not completed**. They'll be documented as they are built and tested.

| Project | Goal | Relevant to |
|---|---|---|
| Backup and restore testing | Prove workloads can be recovered on a tested procedure, not assumption | Sysadmin, Incident Response |
| VLAN segmentation on managed switch | Isolate lab networks behind pfSense without changing the household router | Network Admin, Security Analyst |
| Logging and threat detection (SIEM) | Centralize logs and build detection and triage exercises with Wazuh | SOC Analyst, Security |
| Monitoring alerts | Add host-down alerting on top of the existing Prometheus / Grafana stack | NOC, SRE |
| Automation with Ansible | Publish sanitized, tested configuration examples | Sysadmin, DevOps |

## Lab hardware

- **Proxmox Node 1:** Lenovo M920q, i5-8500T, **32GB RAM** (running, cluster primary)
- **Proxmox Node 2:** Lenovo M920q, i5-8600T, **16GB RAM** (running, joined cluster)
- **Firewall:** Lanner NCA-1515, Atom C3758, 16GB ECC, 128GB SSD (pfSense CE deployed)
- **Switch:** Aruba Instant On 1830 8G (deployed, VLAN config pending)
- **Rack:** DeskPi RackMate T1 Plus, 8U (owned)

Node 1 and Node 2 have asymmetric RAM. Workload placement reflects this.

See [hardware.md](hardware.md) for the appliance inventory.

## How to review this portfolio

Each project explains **the problem, technical decisions, implementation, troubleshooting, validation, and lessons learned**. Work in progress is labeled clearly.

## Connect

- LinkedIn: [linkedin.com/in/martin-capula](https://www.linkedin.com/in/martin-capula)
- Other work: [Healthcare Patient Flow Dashboard](https://github.com/MartinShadow734/healthcare-patient-flow-dashboard)
