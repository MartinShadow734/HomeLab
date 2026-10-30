# Project 01: Proxmox Virtualization

**Status:** In progress  
**Date completed:** Not yet  
**Skills:** Type 1 hypervisor, VM lifecycle management, VM migration, headless Linux administration, remote access  
**Relevant to:** Systems Administrator, NOC Technician, IT Support

## Objective

Turn a used mini PC into a dedicated virtualization host so I can run servers, firewalls, and security tools as isolated virtual machines. In real IT environments almost every server is virtual, so knowing how to build, manage, and recover VMs on a hypervisor is a core skill for sysadmin, NOC, and security roles.

## Architecture

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

### Baseline audit (read-only)

Before changing anything on the host, I ran a read-only baseline audit over SSH to document exactly what the system was and confirm it was healthy. Auditing before touching anything is basic operational discipline: you cannot safely change or troubleshoot a system you have not measured.

Using only non-destructive commands, I inventoried:

- **Compute:** CPU model, core and thread count, and hardware virtualization support (confirming the host can run accelerated VMs)
- **Memory:** total RAM, how much was committed to running workloads, and available headroom
- **Storage:** disk type and size, the storage layout, and free space
- **Workloads:** the virtual machines currently running and their resource assignments
- **Network and access:** host addressing and confirmation that encrypted remote access was working

Every command only read system state; none modified the host. I recorded the results in a private baseline inventory so future changes can be measured against a known-good starting point.

**Key outcome:** the audit surfaced a single point of failure, the host runs on one disk with no redundancy, which set the priority for the next project (backups and a tested restore). A baseline audit is only useful if it changes what you do next; this one did.

### Verifying no unauthorized access

During the audit I treated an earlier concern, unexpected terminal output during a remote session, as a security question rather than assuming it was harmless. I reviewed:

- Current and recent login sessions and their source addresses
- Failed and invalid login attempts
- The accounts and keys authorized to reach the host

All access traced back to my own devices and known networks: no logins from unfamiliar addresses, and no unexpected authorized keys. The "unexpected output" turned out to be a benign terminal display artifact, confirmed by the fact that it tracked my own input rather than a remote actor.

**Lesson:** the first step in responding to anything suspicious is measuring your own exposure from the logs, not guessing. A scary-looking symptom with a clean audit trail is a very different situation from one without, and documenting the check matters as much as the result.

## Troubleshooting and case studies

| Problem | Cause | Fix | Status |
|---|---|---|---|
| Couldn't reach the Proxmox web UI or VMs from outside the house | A private LAN address only works on the home network | Tailscale overlay network, with Termius for mobile SSH | Solved |
| Moving existing VMs off a desktop hypervisor | VirtualBox ties VMs to an everyday workstation | Migrated workloads to Proxmox | Done, procedure being documented |
| SSH from my main Windows PC to a Linux VM fails, while Tailscale SSH works | Under investigation, likely a host firewall rule | [Live troubleshooting log: issue #5](https://github.com/MartinShadow734/HomeLab/issues/5) | Open |
| A disclosed VPN SSH advisory could let an already-authorized device exceed its intended privileges | Affects the built-in Tailscale SSH feature when enabled; vendor confirmed the issues are post-authentication | Verified the feature was already disabled on all hosts; removed an unused SSH access rule | Mitigated |

### Case study: Remote access from outside the home network

**Problem:** I needed to manage the lab when away from home. Opening the Proxmox web interface by its home LAN address from my laptop outside the house didn't work. I also wanted terminal access from my phone instead of needing to be at the server.

**Why it failed:** a private LAN address is scoped to the local network. It isn't reachable across the internet, so knowing the server's address isn't enough.

**Solution:** I used Tailscale to create an encrypted, WireGuard-based private network between my authorized devices and the lab VMs, and Termius on mobile as the SSH client. This gave me remote administration without opening any ports on the home router.

**Key distinction:** Termius is the SSH client, Tailscale provides network reachability. They solve different problems, and confusing the two is a common remote-access mistake.

**Validated through use:**
- Remote SSH administration of Linux VMs over Tailscale
- SSH from mobile using Termius
- No router port forwarding added

**Still to verify:** whether the Proxmox host itself runs Tailscale, and which path reaches the Proxmox web UI remotely. A controlled off-network test will document which routes succeed.

**Lesson:** separate *application access* (web UI, SSH) from *network reachability* (LAN vs VPN). Tailscale also doesn't replace patching, strong authentication, or host firewalls.

### Case study: Migrating from VirtualBox to Proxmox

**Problem:** my Linux workloads ran in VirtualBox on a general-purpose computer, so they depended on that machine being on and in use.

**Approach:** I installed Proxmox VE on the dedicated M920q and moved existing workloads onto it, including a headless Ubuntu Server VM and a second workload migrated from VirtualBox.

**Why a migration is a better test than a fresh install:** moving a VM exercises virtual disk formats, boot compatibility, and virtual NIC changes, not just a clean setup.

**Still to document:** the exact export and import procedure, source and destination VM settings from the live host, and post-migration checks (boot, network, application, persistence after reboot).

**Lesson:** a migration isn't done just because the disk imports. Boot, network reachability, and application behavior all need to be verified.

### Case study: Responding to a disclosed VPN SSH advisory

**Status:** Exposure assessed and mitigated. No compromise found.

**Trigger:** In October 2026, researchers disclosed "Tailworm," a set of reported flaws in the built-in SSH feature of the mesh VPN I use for remote access. The most serious chain would let an already-trusted device on the mesh escalate to root on other nodes. I treated the report as something to assess against my own setup, not as proof my lab was affected.

**First question: am I even running the affected feature?** The main risk depends on the VPN's built-in SSH server. I checked every Linux host:

```bash
sudo tailscale debug prefs | grep -i RunSSH
```

All returned `RunSSH: false`. I use standard OpenSSH over the VPN rather than its built-in SSH feature, so my hosts were not exposed to the main escalation chain.

**Separating researcher claims from vendor-confirmed scope:** The initial writeup framed this as a root-escalation worm. The vendor's own interim statement was more measured: the confirmed issues are post-authentication, affecting how Unix privileges and SSH forwarding are handled after a device is already authorized, not an unauthenticated attacker reaching arbitrary machines. The vendor did not recommend disabling the feature, and its strongest interim mitigation (disabling SSH forwarding) only applies to hosts actually running the built-in SSH server, which mine were not. A full advisory with affected versions and patches was still pending. Reading the vendor assessment alongside the researcher report, instead of acting on the headline alone, is part of responding to any disclosure.

**What I changed:** Following least privilege, I removed an unused SSH access rule from the VPN's access controls to shrink the attack surface further.

**What I did not assume:** Disabling one feature does not resolve every finding or prove the lab is safe. I noted follow-ups: review the full access policy, enable node-key expiration, and watch for an official fix, since at the time there was no patch or CVE.

**Lesson:** The first step in responding to any advisory is measuring your own exposure. "Am I running the affected feature, in the affected version, in the affected configuration?" turned a scary headline into a five-minute verification. Documenting the check matters as much as the fix.

## Validation

- [x] Baseline audit confirms CPU, memory, storage, and VM resource assignments
- [ ] All VMs start cleanly after a host reboot
- [x] Remote SSH access works over Tailscale, including from mobile
- [ ] Network configuration documented and diagrammed

## Lessons learned

- Running workloads in VMs on a Type 1 hypervisor, instead of directly on the host, keeps the host clean and makes each service easy to rebuild or roll back.

## Next improvements

- Complete a read-only baseline audit and publish sanitized results
- Set up scheduled backups to a separate disk and test a full restore (Project 02)
- Make the network bridge VLAN-aware for lab segmentation (Project 04)

## Related job skills

VM provisioning, migration, and remote administration are day-one tasks for sysadmins. Knowing how a hypervisor's storage and networking fit together is also essential when troubleshooting outages as a NOC technician.
