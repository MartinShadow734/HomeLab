# Case study in progress: SSH connectivity diagnosis

**Status:** Unresolved, root cause not yet verified.  
**Skills:** SSH, Linux firewalling, network diagnostics, VPN routing

## Problem
My main Windows PC could not connect to a Linux VM using SSH, although SSH access through Tailscale had worked from other devices.

## Working hypothesis
A Linux UFW rule might allow TCP port 22 on the Tailscale interface while denying it from the local LAN. This is a hypothesis, not a confirmed root cause.

## Troubleshooting plan
1. Compare the destination addresses and paths used by Windows, Termius, and other working clients.
2. Check whether the SSH service is listening and on which interfaces.
3. Inspect UFW status and rules, without changing them.
4. Test network reachability and TCP 22 from the Windows PC.
5. Correlate SSH authentication logs with connection attempts.
6. Make a targeted change only after preserving working access and establishing a rollback path.

## Read-only evidence to collect privately
On the Linux VM: `sudo ss -tlnp`, `sudo ufw status verbose`, `sudo systemctl status ssh`.

On Windows PowerShell: `Test-NetConnection <VM-LAN-IP> -Port 22` and `Test-NetConnection <VM-TAILSCALE-IP> -Port 22`.

These commands inspect listening sockets, firewall policy, SSH service state, and network reachability. Do not publish raw addresses or logs.

## Publication criteria
Update with actual cause, corrective action, and before/after verification once solved. Do not portray the issue as resolved yet.
