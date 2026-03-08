# 🌐 VLAN Design

---

## VLAN Table

| VLAN | Name | Subnet | MTU | Purpose |
|------|------|--------|-----|---------|
| 10 | MGMT | 10.0.10.0/24 | 1500 | iDRAC, iLO, switch management |
| 20 | LAN | 10.0.20.0/24 | 1500 | Workstations, domain traffic |
| 30 | SERVERS | 10.0.30.0/24 | 1500 | VM traffic |
| 40 | STORAGE | 10.0.40.0/24 | 9000 | NFS/iSCSI (jumbo frames) |
| 50 | DMZ | 10.0.50.0/24 | 1500 | Exposed services |
| 99 | WIFI | 10.0.99.0/24 | 1500 | Wireless clients |

---

## IP Allocation — VLAN 10 MGMT (10.0.10.0/24)

| IP | Device | Role |
|----|--------|------|
| 10.0.10.1 | Cisco 3560-CG | Default gateway |
| 10.0.10.2 | DC01 iDRAC | Dell T330 OOB |
| 10.0.10.3 | esxi-01 iDRAC | Dell R620 OOB |
| 10.0.10.4 | esxi-02 iDRAC | Dell R620 OOB |
| 10.0.10.5 | mgmt-01 iLO | HP DL360 G9 OOB |
| 10.0.10.10 | Cisco 891F | Router management |
| 10.0.10.11 | Cisco 3560-CG | Switch management |
| 10.0.10.12 | D-Link DGS-1100 | OOB switch management |

## IP Allocation — VLAN 20 LAN (10.0.20.0/24)

| IP | Device | Role |
|----|--------|------|
| 10.0.20.1 | Cisco 3560-CG | Default gateway |
| 10.0.20.2 | DC01 | Domain Controller |
| 10.0.20.3 | esxi-01 | ESXi host |
| 10.0.20.4 | esxi-02 | ESXi host |
| 10.0.20.5 | mgmt-01 | vCenter/Management |
| 10.0.20.10 | T470s (PAW) | Admin workstation |
| 10.0.20.100-200 | DHCP Pool | Dynamic clients |

---

## Cable Colour Convention

| Colour | VLAN | Purpose |
|--------|------|---------|
| 🔵 Blue | MGMT (10) | OOB management |
| ⚫ Black | LAN (20) | General LAN |
| 🟡 Yellow | SERVERS (30) | VM/server traffic |
| 🟢 Green | STORAGE (40) | NFS/iSCSI |
| 🔴 Red | WAN | Internet uplink |
| ⚪ White | DMZ (50) | Exposed services |

---

*Last updated: 2026-03-08*
