# Case study: Migrating workloads from VirtualBox to Proxmox

**Status:** Migration performed; detailed procedure and verification pending.
**Skills:** Virtualization, VM migration, Linux administration, infrastructure consolidation

## Problem
I initially ran Linux workloads using VirtualBox on a general-purpose computer. I wanted a dedicated virtualization host where VMs could run independently of my everyday workstation.

## Approach
I installed Proxmox VE on a Lenovo ThinkCentre M920q Tiny and moved existing virtualized workloads into that environment. The lab includes a headless Ubuntu Server VM and a separate Career Ops workload migrated from VirtualBox.

## Why this architecture
- Proxmox is a dedicated bare-metal virtualization platform, rather than a desktop application.
- Centralized VM management makes it easier to operate multiple workloads on one physical host.
- Moving existing workloads tests more than a fresh installation: virtual disk formats, boot compatibility, virtual NICs, and service continuity can matter.

## Work performed
- Deployed Proxmox VE on the dedicated Lenovo host.
- Established Linux VM administration.
- Migrated existing VirtualBox workload(s), including Career Ops, to Proxmox.

## Evidence still needed
- Confirm source and destination VM configuration from the actual host.
- Record the exact migration/export/import procedure from notes or logs, without guessing.
- Verify boot, guest network connectivity, applications, and persistence after restart.
- Document any specific migration error only when supported by logs or recalled troubleshooting details.

## Lessons
A VM migration is not complete merely because the disk imports. Boot, network reachability, and application behavior should be validated before declaring success.
