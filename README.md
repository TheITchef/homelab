# 🍳 theITchef HomeLab

> *From physical rack to hybrid cloud — built from scratch.*

[![GitHub](https://img.shields.io/badge/github-TheITchef-black?logo=github)](https://github.com/TheITchef)
[![LinkedIn](https://img.shields.io/badge/linkedin-theITchef-blue?logo=linkedin)](https://linkedin.com/in/theITchef)
[![Domain](https://img.shields.io/badge/web-theITchef.com-orange)](https://theitchef.com)

---

## 🎯 Project Goal

Build a production-grade hybrid cloud home lab that mirrors real enterprise Microsoft infrastructure — combining physical hardware, VMware virtualisation, Microsoft identity services, Cisco networking, Azure hybrid cloud, SRE practices, containers, and ML/AI workflows.

**Design principles:**
- GDPR compliant by design — EU data residency wherever possible
- Security first — zero-trust, MFA, break-glass procedures from day one
- Infrastructure as Code — everything documented and repeatable
- Observability built in — monitoring and logging from the start

---

## 🏗️ Architecture Overview

```
Internet
    │
Cisco 891F (WAN/Edge)
    │
Cisco 3560-CG (L3 Core Switch)
    │
    ├── VLAN 10  MGMT      (10.0.10.0/24)
    ├── VLAN 20  LAN       (10.0.20.0/24)
    ├── VLAN 30  SERVERS   (10.0.30.0/24)
    ├── VLAN 40  STORAGE   (10.0.40.0/24)
    ├── VLAN 50  DMZ       (10.0.50.0/24)
    └── VLAN 99  WIFI      (10.0.99.0/24)

On-premises:
├── DC01      (T330)      — AD DS, DNS, DHCP
├── esxi-01   (R620)      — VMware ESXi
├── esxi-02   (R620)      — VMware ESXi (primary)
└── mgmt-01   (DL360 G9)  — vCenter Server

Azure (Sweden Central):
├── Entra ID              — Azure AD Connect sync
├── Azure Arc             — Hybrid server management
├── Azure VPN Gateway     — Site-to-site IKEv2
└── AKS                   — Azure Kubernetes Service
```

---

## 📁 Repository Structure

```
homelab/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── design-principles.md
│   ├── vlan-design.md
│   └── roadmap.md
├── inventory/
│   ├── hardware-inventory.md
│   └── network-inventory.md
├── network/
│   ├── cabling-plan.md
│   └── rack-layout.md
├── security/
│   └── security-practices.md
├── configs/
│   ├── windows/
│   │   └── dc01-promotion.ps1
│   ├── cisco/
│   └── esxi/
├── scripts/
└── kanban/
    └── KANBAN.md
```

---

## 🖥️ Hardware

| Host | Model | CPU | RAM | Role |
|------|-------|-----|-----|------|
| DC01 | Dell T330 | E3-1220 v6 | 8GB DDR4 | AD DS / DNS / DHCP |
| esxi-01 | Dell R620 | 2× E5-2670 | 128GB DDR3 | VMware ESXi |
| esxi-02 | Dell R620 | 2× E5-2660 | 272GB DDR3 | VMware ESXi (primary) |
| mgmt-01 | HP DL360 G9 | 2× E5-2630v3 | 256GB DDR4 | vCenter / Management |

**Total: 52 cores / 104 threads / 664GB RAM**

---

## 🗺️ Phases

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Physical build, cabling, DC01 | 🔄 In Progress |
| 2 | ESXi cluster, vCenter, storage | ⏳ Planned |
| 3 | Infrastructure services, monitoring, SCCM | ⏳ Planned |
| 4 | Hybrid cloud, Azure Arc, AD Connect | ⏳ Planned |
| 5 | Containers, K8s, databases, ML/AI | ⏳ Planned |

---

## 📋 Design Principles

| # | Principle |
|---|-----------|
| 1 | Prefer EU GDPR compliant solutions by default |
| 2 | Azure deployments → Sweden Central (primary), Sweden South (DR) |
| 3 | Terraform state → EU region or self-hosted MinIO |
| 4 | Personal data never leaves EU boundary |
| 5 | Security first — zero-trust, MFA, break-glass from day one |

---

*Built with ☕ and 🌶️ in Upplands Väsby, Sweden 🇸🇪*
