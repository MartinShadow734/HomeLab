# Project 01: Proxmox Virtualization

**Status:** In progress  
**Date completed:** Not yet  
**Skills:** Type 1 hypervisor, VM lifecycle management, VM migration, headless Linux administration, remote access  
**Relevant to:** Systems Administrator, NOC Technician, IT Support

## Objective

Turn a used mini PC into a dedicated virtualization host so I can run servers, firewalls, and security tools as isolated virtual machines. In real IT environments almost every server is virtual, so knowing how to build, manage, and recover VMs on a hypervisor is a core skill for sysadmin, NOC, and security roles.

## Architecture

<!-- After the audit, add a diagram: ![Proxmox host and VMs](images/proxmox-overview.png) -->

| Component | Role |
|---|---|
| Lenovo ThinkCentre M920q Tiny, i5-8500T | Physical host |
| Proxmox VE | Type 1 hypervisor, managed through its web interface and SSH |
| Ubuntu Server VM (headless) | General-purpose Linux server for administration practice |
| Second Linux VM | Workload migrated from VirtualBox |
| Tailscale | Encrypted remote access to the VMs |

## Tools and technologies

- **Proxmox VE:** bare-metal hypervisor with a web UI for creating and managing VMs
- **Ubuntu Server:** headless Linux, administered entirely over SSH
- **SSH:** remote command-line administration
- **Tailscale:** WireGuard-based mesh VPN for remote access without opening ports on the home router

## Work completed

- Wiped the mini PC and installed Proxmox VE as a dedicated hypervisor
- Built and ran a headless Ubuntu Server VM with no desktop environment
- Migrated an existing VM from VirtualBox (a Type 2 desktop hypervisor) to Proxmox
- Set up SSH and Tailscale for remote administration of the VMs

## Implementation

<!-- Fill in after the baseline audit with real, sanitized output. Suggested steps:
### Step 1: Install Proxmox VE
### Step 2: Create the Ubuntu Server VM (CPU, RAM, disk choices and why)
### Step 3: Migrate the VirtualBox VM (export format, import method)
### Step 4: Remote access with SSH and Tailscale
Add a screenshot per step in images/ and explain each key command.
-->

*Detailed steps and screenshots will be added after the baseline audit.*

## Real-world case studies

- [Remote access using Tailscale and Termius](REMOTE-ACCESS.md): working solution to remote Linux administration, with Proxmox host access pending verification.
- [VirtualBox to Proxmox migration](MIGRATION.md): migration performed; technical evidence being collected.
- [SSH connectivity troubleshooting](SSH-TROUBLESHOOTING.md): ongoing investigation, not yet resolved.

## Troubleshooting

| Problem | Cause | Fix |
|---|---|---|
| SSH from my main PC to the Linux VM stopped working while SSH over Tailscale still worked | Under investigation. Likely a host firewall rule that limits SSH to the Tailscale interface | To be documented |

## Validation

- [ ] Baseline audit confirms CPU, memory, storage, and VM resource assignments
- [ ] All VMs start cleanly after a host reboot
- [ ] Remote SSH access works over Tailscale
- [ ] Network configuration documented and diagrammed

## Lessons learned

- Running workloads in VMs on a Type 1 hypervisor, instead of directly on the host, keeps the host clean and makes each service easy to rebuild or roll back.

## Next improvements

- Complete a read-only baseline audit and publish sanitized results
- Set up scheduled backups to a separate disk and test a full restore (Project 02)
- Make the network bridge VLAN-aware for lab segmentation (Project 04)

## Related job skills

VM provisioning, migration, and remote administration are day-one tasks for sysadmins. Knowing how a hypervisor's storage and networking fit together is also essential when troubleshooting outages as a NOC technician.
