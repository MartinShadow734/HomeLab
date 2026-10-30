# Project 02: Linux Hardening and Security Auditing

**Status:** In progress (host-level hardening complete; SSH key migration and patching pending)
**Skills:** Security auditing, Linux hardening, host-based intrusion prevention, rootkit detection, measure-fix-verify methodology, defense in depth
**Relevant to:** Security Analyst, NOC Technician, Systems Administrator

## Objective

Harden the lab's Linux systems against common attacks and, just as importantly, **measure** the improvement rather than guessing at it. The goal was a repeatable process I could apply to any host: baseline the system, apply fixes, and verify each one actually took effect.

## Approach: measure, fix, verify

I used **Lynis**, an open-source security auditing tool, to produce a numeric **hardening index (0 to 100)** for each host. The workflow on every machine was the same:

1. **Baseline scan** to get a starting score and a list of findings
2. **Apply targeted fixes** (safe, non-disruptive ones first)
3. **Re-scan** to confirm each fix cleared its finding and the score moved
4. Repeat

This "scan, fix, re-scan" loop is how hardening is actually done in a real environment, and it produces evidence instead of assumptions.

## What I implemented

Applied the same hardening playbook across two different systems (a Debian-based hypervisor host and an Ubuntu VM):

- **Host-based intrusion prevention:** installed and enabled **fail2ban**, which automatically bans IP addresses after repeated failed logins. Configured it the correct way (in `jail.local`) so settings survive package updates.
- **Rootkit and malware detection:** installed **rkhunter** and set a known-good file baseline for future comparison.
- **Legal login banners:** added authorized-access warning banners (`/etc/issue`, `/etc/issue.net`).
- **Verification:** re-scanned after each change to confirm it registered.

## Results

| Host | Before | After | Change |
|---|---|---|---|
| Hypervisor host (Debian) | 60 | 64 | +4 |
| Application VM (Ubuntu) | 64 | 67 | +3 |

The same process, applied to two different Linux distributions, measurably improved both. Remaining gains (SSH configuration hardening and full patching) are deliberately staged for a maintenance window because they require setting up key-based authentication first and a reboot.

## Troubleshooting and lessons

### A fix that did not take the first time

After writing a login banner, the re-scan **still flagged it as weak**. Rather than assume the change worked, the re-scan caught that it had not. The auditing tool checks banner content against specific legal-warning keywords, and the first wording did not meet the threshold. A stronger banner cleared it on the next scan.

**Lesson:** never assume a fix worked because the command ran without error. Verify it. Re-scanning is what turned "I think I fixed it" into "I confirmed I fixed it."

### Knowing which findings do not apply

On the hypervisor, the scanner flagged several network interfaces as being in "promiscuous mode." On most systems that is worth investigating, but on a hypervisor it is **expected**, those are the virtual network interfaces that bridge traffic to the VMs. Treating every finding as a problem would have meant "fixing" something that must stay as it is.

**Lesson:** a scanner reports findings without understanding context. Part of the skill is distinguishing a real issue from an expected condition for that system's role.

### An install that silently waited for input

Installing one package dropped into an interactive configuration menu and the install simply paused there until answered. A command that appears to "hang" is sometimes waiting on a prompt.

**Lesson:** when a terminal task stalls, check whether it is actually waiting on input before assuming it failed.

## Where this fits: defense in depth

Host hardening is **one layer**. Securing a system fully means layering defenses:

| Layer | Protected by | Status |
|---|---|---|
| Each host | Hardening (this project) | Host-level done |
| The network | Firewall, VLAN segmentation, IDS/IPS | Planned (needs managed switch) |
| The whole environment | Central monitoring (SIEM) | Planned |

Hardening a host does not secure the network it sits on, and it does not automatically protect the VMs running on it, each system is hardened independently. That separation is why these are distinct projects.

## Validation

- [x] Baseline hardening score captured for each host
- [x] fail2ban installed, enabled, and configured to survive updates
- [x] Rootkit/malware scanner installed with a known-good baseline
- [x] Each fix verified by re-scan
- [ ] SSH configuration hardened (after key-based auth is in place)
- [ ] Systems fully patched and rebooted
- [ ] Playbook extended to remaining VMs

## Related job skills

Security auditing, host hardening, and intrusion prevention are daily work for a Security Analyst, and the measure-fix-verify discipline applies directly to vulnerability management. Running a consistent, repeatable process across multiple systems is exactly what scales in a real environment, and is the foundation for later automating it with configuration management.
