# Hardware

## Parts list

| Item | Model | Role | Status |
|---|---|---|---|
| Rack | DeskPi RackMate T1 Plus, 10-inch 8U, 260 mm deep | Planned rack enclosure | Owned, assembly not verified |
| Server | Lenovo ThinkCentre M920q Tiny, Intel i5-8500T (6C/6T), 1x Intel I219-LM 1GbE NIC | Proxmox VE hypervisor | In use |
| Switch | HPE Aruba Instant On 1830 8G (JL810A), 8x 1GbE, fanless | Lab switching, VLANs, port mirroring | Ordered |
| Server mount | 10-inch 1U ThinkCentre Tiny rack mount | Mounts the M920q flush in the rack | Ordered |
| Patch panel | DeskPi 10-inch 12-port keystone panel | Clean front-of-rack cabling | Ordered |
| Keystones | Cat6 female-to-female couplers | Patch panel ports | Ordered |
| Patch cables | Cat6, 1 ft | Panel to switch | Ordered |
| Power | Tripp Lite TLP606B, 6 outlets | Surge protection | Ordered |

Server memory and storage will be confirmed in the baseline audit and listed here.

## Why these parts

- **Aruba Instant On 1830 over a cheaper MikroTik switch:** the Aruba supports HTTPS management, a dedicated management VLAN, and 802.1X. Some low-cost switches only offer unencrypted HTTP management, which is a bad habit to build in a security lab.
- **One mini PC instead of a rack server:** low power, silent, and fits a 10-inch rack. The tradeoff is limited RAM and a single NIC, so labs run in rotation and all lab VLANs share one 802.1Q trunk.
- **Household network stays untouched:** the lab sits behind the home router. A broken lab never takes the house offline.

## Rack layout

*Photo coming after the physical build.*

| U | Device |
|---|---|
| 1 | Patch panel |
| 2 | Switch (shelf) |
| 3 | M920q (Tiny mount) |
| 4-8 | Blank, room to grow |

*Layout is a draft and will be updated after the build.*

## Known constraints

- **Single NIC:** all lab networks share one trunk port. Sending mirrored traffic to a dedicated capture interface will need a second NIC (PCIe riser or M.2 adapter) later.
- **RAM:** the host can't run every lab at once, so projects run in rotation.
