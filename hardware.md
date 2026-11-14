# Homelab Hardware

| Appliance | Specifications | Status |
|---|---|---|
| Proxmox Node 1 | Lenovo M920q Tiny, i5-8500T, **32GB RAM**, 256GB NVMe | Running; cluster primary |
| Proxmox Node 2 | Lenovo M920q Tiny, i5-8600T, **16GB RAM** | Running; joined cluster |
| Firewall | Lanner NCA-1515, Atom C3758, 16GB ECC RAM, 128GB SSD | Deployed with pfSense CE |
| Managed switch | Aruba Instant On 1830 8G | Deployed; VLAN configuration pending |
| Rack | DeskPi RackMate T1 Plus, 10-inch 8U | Owned |

The existing eero remains the household router. The pfSense firewall is deployed on the Lanner appliance; VLAN segmentation on the Aruba managed switch is the next network milestone.

Node 1 and Node 2 have asymmetric RAM (32GB and 16GB). Workload placement reflects this: heavier VMs run on Node 1, lighter services on Node 2. Live migration from Node 1 to Node 2 is not possible for VMs whose memory exceeds Node 2's capacity.
