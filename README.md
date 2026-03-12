# theITchef HomeLab

**Owner:** Ioannis (theITchef) | **Domain:** ad.theitchef.com | **Azure:** Sweden Central  
**Status:** 🔧 Active build — Phase 1 rack & stack

---

## Purpose

Production-grade hybrid cloud homelab mirroring real enterprise Microsoft infrastructure.  
Goal: accelerate path to infrastructure/cloud consultancy under [theITchef.com](https://theitchef.com).

**Design principles:** GDPR compliant · EU data residency · Security first · IaC everything · Open source first

---

## Hardware

### Servers

| Hostname | Model | Serial | CPU | RAM | Role |
|----------|-------|--------|-----|-----|------|
| itc-uvy-dc-01 | Dell PowerEdge T330 | 3W0MYQ2 | E3-1220 v6 | 8GB DDR4 | AD / DNS |
| itc-uvy-esxi-01 | Dell PowerEdge R620 | 1CCL5Y1 | 2× E5-2660 (32t) | 304GB DDR3 | VMware ESXi 8 |
| itc-uvy-prx-01 | Dell PowerEdge R620 | H2718X1 | 2× E5-2670 (32t) | 96GB DDR3 | Proxmox |
| itc-uvy-sccm-01 | HP ProLiant DL360 Gen9 | CZJ54302TB | 2× E5-2630v3 (32t) | 256GB DDR4 | SCCM / mgmt plane |

**Cluster totals:** 52 cores / 104 threads / 664GB RAM / ~4TB SSD

### Networking

| Hostname | Model | Role |
|----------|-------|------|
| itc-uvy-rtr-01 | Cisco 891F ISR | Edge router / WAN / NAT |
| itc-uvy-sw-01 | Cisco 3560-CG PoE | OOB management switch |
| itc-uvy-sw-02 | Cisco 3850-48P-E | Core L3 switch (ordered) |

---

## Network Design

| VLAN | Name | Subnet | Gateway |
|------|------|--------|---------|
| 10 | MGMT | 10.0.10.0/24 | 10.0.10.1 |
| 20 | LAN | 10.0.20.0/24 | 10.0.20.1 |
| 30 | SERVERS | 10.0.30.0/24 | 10.0.30.1 |
| 40 | STORAGE | 10.0.40.0/24 | 10.0.40.1 |
| 50 | DMZ | 10.0.50.0/24 | 10.0.50.1 |
| 99 | WIFI | 10.0.99.0/24 | 10.0.99.1 |
| 999 | NATIVE | — | Hardened native VLAN |

---

## Repository Structure

```
homelab/
├── configs/cisco/          # 891F + 3560-CG running configs
├── docs/                   # Design docs, rack diagram, port mapping
├── inventory/              # Hardware inventory
├── kanban/                 # Project kanban
├── lessons-learned/        # Weekly lessons
├── linkedin-posts/         # Published posts
├── network/                # VLAN design, rack layout
└── security/               # Security practices
```

---

## Current Phase

- [x] AD DS promoted + hardened
- [x] iDRAC / iLO hardened on all servers
- [x] Cisco 891F configured
- [x] Cisco 3560-CG configured (demoted to OOB)
- [x] PAW (T470s) connected + DNS working
- [x] RAM swap complete (esxi-01: 304GB, prx-01: 96GB)
- [x] Cisco 3850-48P-E ordered
- [ ] 3850 configure as core L3
- [ ] Physical rack build + cabling
- [ ] Proxmox install on prx-01
- [ ] WS2022 eval install on sccm-01
- [ ] vCenter on esxi-01
