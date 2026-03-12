# Port Mapping — theITchef HomeLab
**Last updated:** 2026-03-12

---

## itc-uvy-rtr-01 — Cisco 891F

| Interface | Connected To | VLAN | IP | Notes |
|-----------|-------------|------|----|-------|
| GE8 | ISP | WAN | DHCP (85.228.52.116/21) | ip nat outside |
| GE0 | itc-uvy-sw-02 (when arrives) / itc-uvy-sw-01 (interim) | Trunk all VLANs | — | Native VLAN 999 |

---

## itc-uvy-sw-01 — Cisco 3560-CG (OOB only)

| Port | Connected To | VLAN | Notes |
|------|-------------|------|-------|
| GE0/1 | itc-uvy-prx-01 NIC1 | 30 | Server data |
| GE0/2 | itc-uvy-esxi-01 NIC1 | 30 | Server data |
| GE0/3 | itc-uvy-sccm-01 NIC1 | 30 | Server data |
| GE0/4 | itc-uvy-dc-01 LAN1 | 20 | Server data |
| GE0/5 | T470s PAW | 20 | Admin workstation |
| GE0/6 | itc-uvy-dc-01 LAN2 | 10 | MGMT network |
| GE0/10 | itc-uvy-rtr-01 GE0 | Trunk | Native VLAN 999 |

**Management IP:** 10.0.10.11/24  
**SSH:** `ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -oCiphers=+aes256-cbc admin@10.0.10.11`  
**Shortcut:** `ssh 3560cg` (configured in ~/.ssh/config on T470s)

---

## itc-uvy-sw-02 — Cisco 3850-48P-E (ordered — pending)

| Port | Connected To | VLAN | Notes |
|------|-------------|------|-------|
| TBC | itc-uvy-rtr-01 GE0 | Trunk | Uplink |
| TBC | itc-uvy-sw-01 | Trunk | OOB switch uplink |
| TBC | itc-uvy-prx-01 | 30 | Server data |
| TBC | itc-uvy-esxi-01 | 30 | Server data |
| TBC | itc-uvy-sccm-01 | 30 | Server data |
| TBC | itc-uvy-dc-01 | 20 | Server data |

**Planned management IP:** 10.0.10.12/24

---

## OOB Management IPs

| Device | OOB | IP |
|--------|-----|----|
| itc-uvy-prx-01 | iDRAC Enterprise | 10.0.10.3 |
| itc-uvy-esxi-01 | iDRAC Enterprise | 10.0.10.4 |
| itc-uvy-sccm-01 | iLO4 Advanced | 10.0.10.5 |
| itc-uvy-dc-01 | iDRAC Basic | 10.0.10.6 |

---

## Server NICs / IP Assignments

| Device | Interface | IP | VLAN | Notes |
|--------|-----------|----|----|-------|
| itc-uvy-dc-01 | LAN1 | 10.0.20.2/24 | 20 | DNS server |
| itc-uvy-dc-01 | LAN2 | 10.0.10.2/24 | 10 | MGMT access |
| itc-uvy-prx-01 | NIC1 | DHCP → 10.0.30.x | 30 | Servers VLAN |
| itc-uvy-esxi-01 | NIC1 | DHCP → 10.0.30.x | 30 | Servers VLAN |
| itc-uvy-sccm-01 | NIC1 | DHCP → 10.0.30.x | 30 | Servers VLAN |

---

## Cable Colour Scheme

| Colour | Length | Use |
|--------|--------|-----|
| 🟣 Magenta | 0.25m | Server data NICs |
| 🔵 Blue | 0.25m | iDRAC / iLO OOB |
| 🔴 Red | 0.25m | vMotion |
| 🟣 Violet | 0.25m | Storage |
| ⬜ White | 0.5m | Patch panel → 3850 |
| 🟢 Green | 0.5m | Uplinks / trunks |
