# Case study: Remote Proxmox and Linux administration

**Status:** Remote access solution used successfully; host-side configuration still needs an audit.  
**Skills:** Remote administration, Tailscale, SSH, network troubleshooting, access control

## Problem
I needed to manage my home virtualization lab when away from my local network. Connecting to the Proxmox web interface by its home LAN address from my laptop outside the house did not work, because a private LAN address is not generally reachable across the internet.

I also wanted terminal access from mobile devices rather than depending on physical access to the server.

## Solution
I adopted Tailscale for encrypted remote connectivity between authorized devices and lab systems. I used Termius on mobile to establish SSH sessions over the Tailscale connection. This let me administer Linux VMs while away from home without configuring inbound router port forwarding.

## Why it worked
- A private LAN address is scoped to the local network and does not automatically provide remote reachability.
- Tailscale establishes a private overlay network between authenticated devices, with encrypted WireGuard-based connectivity.
- Termius is the SSH client; Tailscale supplies network reachability. They solve different problems.
- The Proxmox management interface and individual VMs can have different remote-access paths. Exact host Tailscale installation and Proxmox web access route still need verification.

## What I validated through use
- Remote SSH administration of Linux VMs via Tailscale.
- SSH access using Termius on mobile.
- Remote administration without adding router port-forwarding rules.

## Evidence to add
- Sanitized diagram showing laptop/mobile -> Tailscale -> Linux VM, with Proxmox host management shown separately until verified.
- Redacted screenshots of successful remote session, with IPs, device names, usernames and tailnet identifiers removed.
- A controlled off-home-network test of Proxmox web access and VM SSH, documenting which routes succeed.

## Lessons
I learned to distinguish application access (Proxmox web UI or SSH) from network reachability (LAN vs VPN). Remote access is not simply a matter of knowing the server's address.

**Security:** This case study intentionally omits IP addresses, internal names, credentials, and access policies. Tailscale does not replace OS patching, strong authentication, or host firewall controls.
