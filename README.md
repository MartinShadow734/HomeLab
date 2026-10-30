# HomeLab | Infrastructure & Security Portfolio

Hands-on projects in **virtualization, Linux administration, networking, and cybersecurity**, built to demonstrate practical IT and troubleshooting skills.

I'm Martin Capula. I work in IT support and am developing toward NOC and security analyst roles. I hold **CompTIA Security+**, **CompTIA A+**, and **ISC2 CC**, and I'm studying for the **CCNA**.

## Start here: Featured project

### [01 · Proxmox Virtualization and VM Migration](projects/01-proxmox-virtualization/README.md)
**In progress** | Proxmox VE · Ubuntu Server · SSH · Tailscale · VirtualBox migration

**Relevant to:** Systems Administrator, NOC Technician, IT Support

**Challenge:** Run and manage multiple server workloads on one compact physical computer rather than relying on a desktop hypervisor.

**What I've done:** Installed Proxmox VE on a Lenovo ThinkCentre M920q Tiny, created a headless Ubuntu Server VM, migrated an existing workload from VirtualBox, and configured remote administration.

**What this demonstrates:** Hypervisor administration, VM migration, Linux CLI, remote connectivity, and systematic troubleshooting.

**Evidence still being prepared:** A read-only host baseline, sanitized architecture diagram, screenshots, and documented validation tests.

[Explore the project →](projects/01-proxmox-virtualization/README.md)

### [02 · Linux Hardening and Security Auditing](projects/02-linux-hardening/README.md)

Hardened two Linux systems with a repeatable measure-fix-verify process using Lynis, fail2ban, and rootkit detection, raising each system's hardening score and documenting the method and lessons learned. **Relevant to:** Security Analyst, NOC, Sysadmin.

[Explore the project →](projects/02-linux-hardening/README.md)

## Skills at a glance

| Area | Hands-on work |
|---|---|
| Virtualization | Proxmox VE, VM deployment and migration |
| Linux | Ubuntu Server, headless administration, SSH |
| Remote access | Tailscale, SSH connectivity troubleshooting |
| Infrastructure planning | Compact rack, hardware selection, planned network segmentation |
| Documentation | Architecture decisions, implementation notes, validation plans |

## What's next

These projects are **planned, not completed**. They'll be documented as they are built and tested.

| Project | Goal | Relevant to |
|---|---|---|
| Backup and restore testing | Prove workloads can be recovered | Sysadmin, Incident Response |
| Rack and managed switch build | Document physical installation and switch baseline | NOC, Field IT |
| VLAN segmentation and OPNsense | Isolate lab networks without changing the household router | Network Admin, Security Analyst |
| Monitoring and security operations | Build observability, logging, and detection exercises | NOC, SOC Analyst |
| Automation with Ansible | Publish sanitized, tested configuration examples | Sysadmin, DevOps |

## Lab hardware

- **Running:** Lenovo ThinkCentre M920q Tiny with Proxmox VE
- **Owned, installation not verified:** DeskPi RackMate T1 Plus 8U rack
- **Ordered, not yet deployed:** Aruba Instant On 1830 8G switch and rack accessories

See the [hardware inventory](hardware.md) for precise component status.

## How to review this portfolio

Each project explains **the problem, technical decisions, implementation, troubleshooting, validation, and lessons learned**. Work in progress is labeled clearly.

## Connect

- LinkedIn: [linkedin.com/in/martin-capula](https://www.linkedin.com/in/martin-capula)
- Other work: [Healthcare Patient Flow Dashboard](https://github.com/MartinShadow734/healthcare-patient-flow-dashboard)
