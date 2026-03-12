# Rack Layout — itc-uvy-rack-01
**Rack model:** HP 10642G2 (42U) | U1 = bottom  
**Last updated:** 2026-03-12

| U | Device | Hostname | Role |
|---|--------|----------|------|
| U42–U35 | Blanking panels | — | — |
| U34 | 24-port Keystone Patch Panel | — | Phase 2 |
| U33 | 1U Cable Manager | — | — |
| U32 | Cisco 891F ISR | itc-uvy-rtr-01 | Edge router / WAN |
| U31 | 1U Cable Manager | — | — |
| U30 | Cisco 3850-48P-E | itc-uvy-sw-02 | Core L3 switch |
| U29 | Cisco 3560-CG | itc-uvy-sw-01 | OOB switch |
| U28 | 1U Shelf | — | D-Link DGS-1100 + TP-Link 5-port |
| U27 | 1U Shelf | — | KVM (temporary) |
| U26–U19 | Blanking panels | — | — |
| U18 | Dell PowerEdge R620 | itc-uvy-prx-01 | Proxmox |
| U17 | Dell PowerEdge R620 | itc-uvy-esxi-01 | VMware ESXi 8 |
| U16–U13 | Blanking panels | — | — |
| U12 | HP ProLiant DL360 Gen9 | itc-uvy-sccm-01 | SCCM / mgmt plane |
| U11 | Blanking panel | — | — |
| U01–U10 | Dell PowerEdge T330 on shelf | itc-uvy-dc-01 | AD / DNS |

## Notes
- 3850 ordered from renewtech.se — pending arrival
- R620 rack rails still awaited from seller
- Phase 2: patch panel + structured cabling (305m Cat6 box)
