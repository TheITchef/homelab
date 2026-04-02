# theITchef HomeLab

**Owner:** Ioannis (theITchef) | **Domain:** ad.theitchef.com | **Azure:** Sweden Central  
**Status:** 🔧 Active build — Phase 1 rack & stack (2026 Architecture Revision)

---

## Purpose

Production‑grade hybrid cloud homelab mirroring real enterprise Microsoft infrastructure.  
Goal: accelerate path to infrastructure/cloud consultancy under theITchef.com.

**Design principles:** GDPR compliant · EU data residency · Security first · IaC everything · Open source first

---

## 2026 Architecture Revision

The 2026 rebuild introduces a major architectural shift:

### ✔️ DL360 Gen9 becomes a **Hyper‑V host only**  
- Runs Windows Server 2025 Datacenter  
- No domain roles on bare metal  
- All Microsoft infrastructure services run as virtual machines

### ✔️ Microsoft services are now fully virtualized  
- Domain Controller  
- DNS  
- Entra Connect  
- SQL Server  
- MECM / SCCM  
- Management jump host  
- Optional: PKI, WSUS, File Server

### ✔️ Network core upgraded  
- Cisco 3850‑48P‑E is now the **active L3 core**  
- All SVIs and east‑west routing moved from 3560 → 3850  
- Cisco 3560‑CG demoted to **OOB‑only**

This aligns the homelab with modern enterprise design patterns and prepares the environment for hybrid identity, MECM, and Azure Arc.

---

## Hardware

### Servers

| Hostname | Model | Serial | CPU | RAM | Role (Revised 2026) |
|----------|-------|--------|-----|-----|----------------------|
| itc‑uvy‑ms‑01 | HP DL360 Gen9 | CZJ54302TB | 2× E5‑2630v3 | 256GB DDR4 | **Hyper‑V host (all Microsoft infra virtualized)** |
| itc‑uvy‑esxi‑01 | Dell PowerEdge R620 | 1CCL5Y1 | 2× E5‑2660 | 304GB DDR3 | VMware ESXi 8 |
| itc‑uvy‑prx‑01 | Dell PowerEdge R620 | H2718X1 | 2× E5‑2670 | 96GB DDR3 | Proxmox |
| itc‑uvy‑dc‑01 | Dell PowerEdge T330 | 3W0MYQ2 | E3‑1220 v6 | 8GB DDR4 | **Legacy — to be demoted** |

### Networking

| Hostname | Model | Role |
|----------|-------|------|
| itc‑uvy‑rtr‑01 | Cisco 891F ISR | Edge router / WAN / NAT |
| itc‑uvy‑sw‑02 | Cisco 3850‑48P‑E | **Core L3 switch (active)** |
| itc‑uvy‑sw‑01 | Cisco 3560‑CG PoE | **OOB management switch** |

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

homelab/
├── configs/cisco/          # 891F + 3560-CG + 3850 configs
├── docs/                   # Design docs, rack diagram, port mapping
├── inventory/              # Hardware inventory
├── kanban/                 # Project kanban
├── lessons-learned/        # Weekly lessons
├── network/                # VLAN design, L3 core migration
└── security/               # Security practices
Code


---

## Current Phase (2026)

- [x] DL360 installed with Windows Server 2025 Datacenter  
- [x] Hyper‑V role enabled (host‑only architecture)  
- [x] Cisco 3850 installed and active as L3 core  
- [x] Cisco 3560 demoted to OOB  
- [ ] Virtualized DC deployment  
- [ ] AD migration from T330 → VM  
- [ ] Entra Connect VM deployment  
- [ ] SQL + MECM VM deployment  
- [ ] vCenter on esxi‑01  
- [ ] Proxmox cluster build on prx‑01  