# Port Mapping — theITchef HomeLab
**Last updated:** 2026-03-11  
**Author:** Ioannis (theITchef)  
> *Verba volant, scripta manent* — if it's not written, it didn't happen.

---

## Cisco 891F ISR — itc-uvy-rtr-01
**Management IP:** 10.0.10.1 (Vlan10 SVI)  
**WAN IP:** 85.228.52.116 (DHCP from ISP)

| Port | Type | Connection | VLAN / Role |
|------|------|-----------|-------------|
| GE8 | WAN | ISP wall port (10m red Cat6) | WAN — ip nat outside |
| GE0 | Trunk | 3560-CG GE0/10 (0.5m) | Trunk — all VLANs, native 999 |
| GE1–GE7 | Internal switch | Unused | — |
| Vlan10 SVI | L3 | — | 10.0.10.1/24 — MGMT gateway |
| Vlan20 SVI | L3 | — | 10.0.20.1/24 — LAN gateway |
| Vlan30 SVI | L3 | — | 10.0.30.1/24 — SERVERS gateway |
| Vlan40 SVI | L3 | — | 10.0.40.1/24 — STORAGE gateway |
| Vlan50 SVI | L3 | — | 10.0.50.1/24 — DMZ gateway |
| Vlan99 SVI | L3 | — | 10.0.99.1/24 — WIFI gateway |

---

## Cisco 3560-CG — itc-uvy-sw-01 (OOB Management only)
**Management IP:** 10.0.10.11 (Vlan10 SVI)  
**Default gateway:** 10.0.10.1  
**Role:** Demoted to OOB management switch after 3850 arrives

| Port | Type | Connection | VLAN / Role |
|------|------|-----------|-------------|
| GE0/1 | Access | esxi-01 data NIC | VLAN 30 SERVERS |
| GE0/2 | Access | esxi-02 data NIC | VLAN 30 SERVERS |
| GE0/3 | Access | mgmt-01 data NIC | VLAN 30 SERVERS |
| GE0/4 | Access | DC01 LAN1 | VLAN 20 LAN |
| GE0/5 | Access | T470s PAW | VLAN 20 LAN |
| GE0/6 | Access | DC01 LAN2 | VLAN 10 MGMT ✅ |
| GE0/7 | Access | Spare | — |
| GE0/8 | Access | Spare | — |
| GE0/9 | SFP combo | Spare | — |
| GE0/10 | Trunk | 891F GE0 (0.5m) | Trunk — all VLANs, native 999 ✅ |
| GE0/11 | Access | Spare | — |
| GE0/12 | Access | Spare | — |

> ⚠️ After 3850 arrives: GE0/1–GE0/5 will be decommissioned from 3560-CG and re-patched to 3850. 3560-CG will only retain OOB ports (iDRAC/iLO).

---

## Cisco 3850-48P-E — itc-uvy-sw-02 (Ordered — not yet configured)
**Planned Management IP:** 10.0.10.12 (Vlan10 SVI)  
**Role:** Core L3 switch — all server and device connectivity

| Port | Type | Planned Connection | VLAN / Role |
|------|------|-------------------|-------------|
| GE1/0/1 | Access | esxi-01 data NIC | VLAN 30 SERVERS |
| GE1/0/2 | Access | esxi-01 vMotion NIC | VLAN 40 STORAGE |
| GE1/0/3 | Access | esxi-02 data NIC | VLAN 30 SERVERS |
| GE1/0/4 | Access | esxi-02 vMotion NIC | VLAN 40 STORAGE |
| GE1/0/5 | Access | mgmt-01 data NIC | VLAN 30 SERVERS |
| GE1/0/6 | Access | DC01 LAN1 | VLAN 20 LAN |
| GE1/0/7 | Access | T470s PAW | VLAN 20 LAN |
| GE1/0/8 | Access | TP-Link 5-port (home WiFi dist.) | VLAN 99 WIFI |
| GE1/0/9 | Access | Spare | — |
| GE1/0/10 | Trunk | 891F GE0 | Trunk — all VLANs, native 999 |
| GE1/0/11–48 | Access | Future expansion | — |

---

## D-Link DGS-1100-08V2 — sw-mgmt-01 (OOB Management)
**Role:** Dedicated OOB switch — iDRAC/iLO only, VLAN 10  
**Planned Management IP:** 10.0.10.20

| Port | Connection | IP |
|------|-----------|-----|
| 1 | esxi-01 iDRAC | 10.0.10.3 |
| 2 | esxi-02 iDRAC | 10.0.10.4 |
| 3 | mgmt-01 iLO4 | 10.0.10.5 |
| 4 | DC01 iDRAC Basic (shared LAN2) | 10.0.10.6 |
| 5 | Spare | — |
| 6 | Spare | — |
| 7 | Spare | — |
| 8 | Uplink → 3560-CG (VLAN 10) | — |

---

## OOB Management — IP Reference
| Device | OOB Type | IP | Username | Notes |
|--------|---------|-----|----------|-------|
| esxi-01 | iDRAC Enterprise | 10.0.10.3 | itchef-admin | root disabled ✅ |
| esxi-02 | iDRAC Enterprise | 10.0.10.4 | itchef-admin | root disabled ✅ |
| mgmt-01 | iLO4 Advanced | 10.0.10.5 | itchef-admin | Administrator secured ✅ |
| DC01 | iDRAC Basic | 10.0.10.6 | — | No web UI, KVM only ⚠️ |
| itc-uvy-sw-01 | SSH | 10.0.10.11 | admin | Legacy SSH flags required |
| itc-uvy-sw-02 | SSH | 10.0.10.12 | admin | Pending config |
| itc-uvy-rtr-01 | SSH | 10.0.10.1 | admin | — |

---

## Device Static IPs — Full Reference
| Device | Interface | IP | VLAN | Role |
|--------|-----------|-----|------|------|
| DC01 | LAN1 | 10.0.20.2 | 20 | AD/DNS |
| DC01 | LAN2 | 10.0.10.2 | 10 | MGMT presence |
| itc-uvy-rtr-01 | Vlan10 | 10.0.10.1 | 10 | MGMT gateway |
| itc-uvy-rtr-01 | Vlan20 | 10.0.20.1 | 20 | LAN gateway |
| itc-uvy-rtr-01 | Vlan30 | 10.0.30.1 | 30 | SERVERS gateway |
| itc-uvy-rtr-01 | Vlan40 | 10.0.40.1 | 40 | STORAGE gateway |
| itc-uvy-rtr-01 | Vlan50 | 10.0.50.1 | 50 | DMZ gateway |
| itc-uvy-rtr-01 | Vlan99 | 10.0.99.1 | 99 | WIFI gateway |
| itc-uvy-sw-01 | Vlan10 | 10.0.10.11 | 10 | Switch mgmt |
| itc-uvy-sw-02 | Vlan10 | 10.0.10.12 | 10 | Switch mgmt (planned) |
| esxi-01 iDRAC | dedicated | 10.0.10.3 | 10 | OOB |
| esxi-02 iDRAC | dedicated | 10.0.10.4 | 10 | OOB |
| mgmt-01 iLO4 | dedicated | 10.0.10.5 | 10 | OOB |
| DC01 iDRAC | shared LAN2 | 10.0.10.6 | 10 | OOB |
| T470s PAW | enp0s31f6 | DHCP 10.0.20.x | 20 | Admin workstation |

---

*Print this document before the rack build. Tick off each cable as it is run.*  
*github.com/TheITchef/homelab · docs/port-mapping.md*
