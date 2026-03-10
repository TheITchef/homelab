# 🏠 theITchef HomeLab

> Production-grade hybrid cloud homelab — mirroring real enterprise Microsoft infrastructure.  
> Built from the ground up during a dedicated engineering bootcamp (March 2026).

**Owner:** Ioannis | **Brand:** [theITchef.com](https://theitchef.com) | **Location:** Upplands Väsby, Sweden  
**Domain:** ad.theitchef.com | **Azure Region:** Sweden Central  
**Last updated:** 2026-03-10

---

## 📁 Repo Structure

```
homelab/
├── README.md                        ← this file
├── inventory/
│   └── hardware-inventory.md        ← full equipment specs & serial numbers
├── docs/
│   ├── design-principles.md         ← architecture decisions & design philosophy
│   ├── vlan-design.md               ← VLAN layout, IP scheme, topology
│   ├── roadmap.md                   ← phase roadmap
│   └── rack-layout.md               ← U-map and physical layout
├── configs/
│   ├── cisco/
│   │   ├── 891f-running-config.txt  ← sanitized router config ✅
│   │   └── 3560cg-running-config.txt← sanitized switch config ✅
│   └── dlink-dgs1100/               ← OOB switch (pending)
├── kanban/
│   └── KANBAN.md                    ← Obsidian Kanban board
├── scripts/                         ← automation scripts (Phase 3)
├── terraform/                       ← IaC (Phase 4)
├── ansible/                         ← automation (Phase 3)
└── linkedin-posts/
    └── post-01-lab-intro.md         ← published ✅
```

---

## 🖥️ Hardware Summary

| Host | Model | CPU | RAM | Role |
|------|-------|-----|-----|------|
| DC01 | Dell T330 | Xeon E3-1220 v6 | 8GB | Domain Controller |
| esxi-01 | Dell R620 | 2× E5-2670 (32t) | 128GB | Hypervisor |
| esxi-02 | Dell R620 | 2× E5-2660 (32t) | 272GB | Hypervisor |
| mgmt-01 | HP DL360 Gen9 | 2× E5-2630v3 (32t) | 256GB | Management |
| itc-uvy-rtr-01 | Cisco 891F ISR | — | — | Edge Router |
| itc-uvy-sw-01 | Cisco 3560-CG | — | — | L3 Core Switch |

**Cluster total: 52 cores / 104 threads / 664GB RAM / 3.84TB SSD**

---

## 🌐 Network Design

| VLAN | Name | Subnet |
|------|------|--------|
| 10 | MGMT | 10.0.10.0/24 |
| 20 | LAN | 10.0.20.0/24 |
| 30 | SERVERS | 10.0.30.0/24 |
| 40 | STORAGE | 10.0.40.0/24 |
| 50 | DMZ | 10.0.50.0/24 |
| 99 | WIFI | 10.0.99.0/24 |
| 999 | NATIVE | — |

---

## 🔗 Phase Roadmap

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Physical build, networking, AD, PAW | 🔄 In Progress |
| 2 | ESXi cluster, vCenter, shared storage | ⏳ Planned |
| 3 | Infrastructure services, monitoring, SCCM | ⏳ Planned |
| 4 | Hybrid cloud — Azure Arc, AD Connect, Terraform | ⏳ Future |
| 5 | Containers, Kubernetes, ML/AI workloads | ⏳ Future |

### ✅ Phase 1 Progress
- [x] Hardware inventory documented
- [x] Active Directory — domain ad.theitchef.com promoted
- [x] AD OU structure, users, service accounts, PSO
- [x] Cisco 891F — full config (NAT, VLANs, ACLs, DHCP, SSH)
- [x] Cisco 3560-CG — full config (VLANs, trunking, port assignments)
- [x] Lab network live — internet via NAT through 891F
- [x] DC01 migrated to lab network (10.0.20.2)
- [x] T470s PAW on lab network, RDP to DC01 working
- [x] DNS persistence fixed on T470s
- [ ] YubiKey MFA setup (keys ordered ✅)
- [ ] Change all iDRAC/iLO default passwords
- [ ] Physical rack build & cabling

---

## 🛡️ Security Note

All configs in this repo are **sanitized** — no passwords, no public IPs, no serial numbers.  
OOB credentials are stored in a local KeePass database only.  
Design principles: zero-trust, MFA from day one, GDPR-compliant EU data residency.

---

## 📅 Update Schedule

This repo is updated **every Monday** with the previous week's progress.  
Kanban board (`kanban/KANBAN.md`) is updated continuously throughout the week.

---

*Follow the journey on LinkedIn → [#theitchef](https://linkedin.com/in/theitchef) | #homelab #cisco #microsoft #hybridcloud*
