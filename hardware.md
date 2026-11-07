# Hardware

This inventory separates purchased hardware from installed and verified infrastructure. The home eero network remains the household router; the lab is built behind it.

## Compute, firewall, and network

| Item | Model and specifications | Intended role | Status |
|---|---|---|---|
| Proxmox node 1 | Lenovo ThinkCentre M920q Tiny; Intel Core i5-8500T (6 cores/6 threads); **32GB DDR4 RAM**; 256GB NVMe SSD; Intel I219-LM 1GbE | Running hypervisor, lab and security workloads | **Running**; RAM and disk confirmed in private host audit |
| Proxmox node 2 | Lenovo ThinkCentre M920q Tiny; Intel Core i5-8500T; **16GB RAM allocated/planned** from node 1's former memory; spare SSD planned | Second hypervisor, future home/self-hosted services | **Purchased**; physical installation, memory fit, SSD and Proxmox setup not yet verified |
| Dedicated firewall | Lanner NCA-1515 (L-1515A); Intel Atom C3758 8-core; **16GB DDR4 ECC**; 128GB SSD; 6x 1GbE RJ45 + 2x SFP | OPNsense firewall, inter-VLAN routing and future Suricata | **Purchased**; delivery, installation and port validation pending |
| Managed switch | Aruba Instant On 1830 8G (JL810A); 8x 1GbE | VLAN-aware switching and lab uplinks | **Ordered**; baseline and configuration pending |
| Household router | Existing eero mesh | Household internet and Wi-Fi, upstream of the lab firewall | **In use**; no changes planned |

**Cluster note:** Matching CPUs do not by themselves provide live migration or high availability. Two-node quorum, a possible QDevice, storage placement and network configuration must be designed and tested before cluster capabilities are claimed.

## Rack, cabling, and power

| Item | Model | Status |
|---|---|---|
| Rack | DeskPi RackMate T1 Plus, 10-inch 8U, 260mm deep | Owned; assembly not verified |
| Node 1 mount | Mesh 3D Lab 10-inch 1U ThinkCentre Tiny sleeve | Purchased; fit not verified |
| Node 2 mount | Second matching 10-inch 1U Tiny sleeve | Needed; not purchased |
| Firewall shelf | 10-inch 1U shelf for Lanner NCA-1515 | Needed; not purchased; measure fit before buying |
| Patch panel | DeskPi 10-inch 12-port keystone panel | Ordered |
| Keystone couplers | VCE Cat6 female-to-female, 5-pack | Ordered |
| Patch cables | Cable Matters Cat6 1-foot, 5-pack | Ordered |
| Surge protector | Tripp Lite TLP606B, 6 outlets | Ordered |
| Longer eero uplink cable | Cat6, length to be measured | Needed; not purchased |
| Backup storage | Separate USB SSD or other independent backup target | Needed; not purchased |

## Proposed network architecture

```text
Frontier Internet
      |
Existing eero (household LAN / Wi-Fi, unchanged)
      |
Lanner NCA-1515 running OPNsense (not yet deployed)
      |
Aruba 1830 managed switch (not yet configured)
      |                  |
M920q node 1       M920q node 2
32GB RAM           16GB RAM planned
```

OPNsense is planned as a **dedicated physical firewall**, not a VM on Proxmox. VLAN IDs, addressing, firewall rules, and management access still need validation. Do not infer that the proposed network is already operating.

## Draft rack layout

| Rack space | Proposed equipment |
|---|---|
| 1U | Keystone patch panel |
| 1U | Aruba switch (shelf or suitable mounting method) |
| 1U | Proxmox node 1 in Tiny sleeve |
| 1U | Proxmox node 2 in second Tiny sleeve |
| 1U | Lanner firewall on a properly sized shelf |
| Remaining 3U | Cable management and future expansion |

The 8U rack plan is **conceptual**. Check real device clearances, shelf widths, cable bend radius, airflow, and power placement before installation.

## Known constraints and priorities

- Node 1 currently has a single 256GB boot/storage drive. Scheduled backups to separate storage and a tested VM restore are the next major resilience priorities.
- Each M920q has one built-in 1GbE NIC. VLAN-aware trunks are planned; management reachability must be preserved during changes.
- A two-node Proxmox cluster needs quorum planning. Shared or migration-compatible storage is not currently verified.
- Prometheus and Grafana are running, but alerting and remaining credential hardening are not finished.
- The Lanner's 16GB RAM provides room to evaluate Suricata later, but IPS throughput and interface compatibility are not yet measured.
