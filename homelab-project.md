# 🏠 HomeLab — Project Hub

> **Status:** 🟡 In Progress  
> **Phase:** 1 — Physical Build, Networking, AD  
> **Repo:** `github.com/TheITchef/homelab`  
> **Last updated:** 2026-03-10

---

## 🗂️ Quick Links

- [[homelab-kanban]] — Kanban Board
- [[homelab-cabling]] — Structured Cabling Guide
- `docs/vlan-design.md` — Network Topology & VLANs
- `docs/rack-diagram.html` — Visual Rack Diagram
- `lessons-learned/` — Engineering journal

---

## 🖥️ Server Roles (FINAL)

| Host | Model | RAM | Role | Track |
|------|-------|-----|------|-------|
| DC01 | Dell T330 | 8GB | AD / DNS — permanent | Microsoft |
| esxi-02 | Dell R620 (1CCL5Y1) | 272GB | ESXi 8 — VMware + Windows VMs + SCCM clients | Microsoft / VMware |
| esxi-01 | Dell R620 (H2718X1) | 128GB | Proxmox — Linux VMs, k3s, SRE/DevOps stack | SRE / DevOps |
| mgmt-01 | HP DL360 Gen9 | 256GB | Windows Server DC — SCCM, SQL, management plane | Microsoft |

---

## 🌐 Three Tracks

### 🔵 Microsoft Track
- Hyper-V / ESXi → Windows Server VMs
- SCCM / MECM (180-day eval)
- Azure Arc, AD Connect
- Hybrid cloud (Phase 4)

### 🟢 SRE / DevOps Track
- Proxmox on esxi-01
- k3s Kubernetes cluster
- Prometheus + Grafana + Alertmanager
- ELK or Loki logging stack
- Terraform + Ansible (IaC)
- GitLab CI/CD
- Docker → Kubernetes progression

### 🔴 Networking Track
- Cisco 891F (edge, WAN, NAT) ✅
- Cisco 3850-48P-E (core L3, 48×PoE+) — ordered
- Cisco 3560-CG (demoted → OOB only) ✅
- FortiGate 60F (under consideration — DPI/NGFW)

---

## 🧱 Equipment Inventory

| Host | Model | CPU | RAM | Storage | Role |
|------|-------|-----|-----|---------|------|
| DC01 | Dell T330 | E3-1220 v6 | 8GB | 1TB HDD | AD/DNS |
| esxi-01 | Dell R620 (H2718X1) | 2×E5-2670 (32t) | 128GB | 480GB SSD | Proxmox |
| esxi-02 | Dell R620 (1CCL5Y1) | 2×E5-2660 (32t) | 272GB | 1.86TB SSD | ESXi 8 |
| mgmt-01 | HP DL360 Gen9 | 2×E5-2630v3 (32t) | 256GB | 1TB SSD | SCCM/mgmt |
| itc-uvy-rtr-01 | Cisco 891F ISR | — | — | — | Edge router |
| itc-uvy-sw-01 | Cisco 3560-CG | — | — | — | OOB switch |
| itc-uvy-sw-02 | Cisco 3850-48P-E | — | — | — | Core L3 switch |

**Cluster total: 52 cores / 104 threads / 664GB RAM / 3.84TB SSD**

---

## 🌐 VLAN Design

| VLAN | Name | Subnet | Purpose |
|------|------|--------|---------|
| 10 | MGMT | 10.0.10.0/24 | iDRAC, iLO, switch mgmt |
| 20 | LAN | 10.0.20.0/24 | Workstations, general |
| 30 | SERVERS | 10.0.30.0/24 | VM production traffic |
| 40 | STORAGE | 10.0.40.0/24 | NFS/iSCSI — MTU 9000 |
| 50 | DMZ | 10.0.50.0/24 | Internet-facing services |
| 99 | WIFI | 10.0.99.0/24 | Wireless clients (isolated) |
| 999 | NATIVE | — | Hardened native VLAN |

---

## 📐 Rack Layout (U-Map)

```
U42  ← top
...
U34  24-port Keystone Patch Panel (Phase 2)
U33  1U Cable Manager
U32  Cisco 891F ISR                [itc-uvy-rtr-01] ✅
U31  1U Cable Manager
U30  Cisco 3850-48P-E              [itc-uvy-sw-02]  ordered
U29  Cisco 3560-CG                 [itc-uvy-sw-01]  OOB only ✅
U28  1U Shelf: D-Link + TP-Link 5-port
U27  1U Shelf: KVM (temporary)
U26–U19  Blanking panels
U18  Dell R620 esxi-01             [Proxmox]
U17  Dell R620 esxi-02             [ESXi 8] ✅
U16–U13  Blanking panels
U12  HP DL360 Gen9 mgmt-01         [SCCM/mgmt]
U11  Blanking panel
U01–U10  Dell T330 DC01 on shelf   [AD/DNS] ✅
```

---

## 🎨 Cable Colour Convention

| Colour | Use |
|--------|-----|
| 🔴 Red 10m | WAN external run |
| 🟢 Green 10m | T470s desk (PAW) |
| ⚫ Black 10m | Spare external |
| 🩶 Panduit grey | All structural rack runs |
| 🟡 Yellow 0.3m | Server data NICs |
| 🔵 Blue 0.3m | OOB / iDRAC / iLO |
| 🟠 Orange 0.3m | vMotion |
| 🟣 Purple 0.3m | Storage |
| 🔴 Red 0.5m | Uplinks / trunks |
| ⬜ White 0.5m | Patch panel front → 3850 |

---

## 🔗 Phase Roadmap

```
Phase 1: Physical Build & Foundation        ← IN PROGRESS
  ├─ Cisco 891F + 3560-CG configured ✅
  ├─ AD/DNS live on DC01 ✅
  ├─ T470s PAW connected ✅
  ├─ iDRAC/iLO hardened (in progress)
  ├─ Cisco 3850-48P-E arriving
  └─ Physical rack build + cabling

Phase 2: Virtualization Layer
  ├─ ESXi 8 on esxi-02 ✅ (update to U3)
  ├─ Proxmox on esxi-01
  ├─ vCenter on esxi-02
  ├─ Shared storage (esxi-02 local + NFS from DC01)
  └─ Patch panel + structured cabling

Phase 3: Infrastructure Services            ← Microsoft + SRE tracks split
  Microsoft:
  ├─ Windows Server DC on mgmt-01
  ├─ SCCM / MECM (180-day eval)
  ├─ SQL Server
  └─ Hyper-V cluster (optional)
  SRE/DevOps:
  ├─ k3s Kubernetes on Proxmox
  ├─ Prometheus + Grafana + Alertmanager
  ├─ Loki or ELK logging
  ├─ Terraform + Ansible
  └─ GitLab CI/CD

Phase 4: Hybrid Cloud                       ← FUTURE
  ├─ Azure Arc (esxi-02 + mgmt-01)
  ├─ AD Connect → Entra ID
  ├─ Site-to-site VPN (IKEv2 via 891F)
  ├─ FortiGate NGFW (if acquired)
  └─ Azure Sweden Central (primary) + Sweden South (DR)

Phase 5: Advanced                           ← FUTURE
  ├─ Service mesh (Istio/Linkerd)
  ├─ ML/AI workloads
  └─ Multi-cloud (AWS/GCP experiments)
```

---

## 📝 Architecture Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-03-06 | DC01 T330 as permanent AD/DNS | Stable, low power, dedicated role |
| 2026-03-06 | Cisco 891F as edge router | Owned, enterprise IOS, VPN capable |
| 2026-03-08 | 3560-CG demoted to OOB only | 3850-48P-E ordered as core L3 |
| 2026-03-10 | esxi-02 → ESXi 8 (VMware track) | 272GB RAM, strongest compute node |
| 2026-03-10 | esxi-01 → Proxmox (SRE track) | Free licence, Linux native, k3s ready |
| 2026-03-10 | mgmt-01 → Windows Server DC (SCCM) | 256GB RAM, dedicated management plane |
| 2026-03-10 | Cabling architecture frozen until Phase 2 | Patch panel + keystone after rack build |
| 2026-03-10 | FortiGate 60F under consideration | SMB NGFW, DPI, strong CV value |

---

*Tags: #homelab #infrastructure #vmware #proxmox #cisco #microsoft #sccm #sre #devops #k8s #hybridcloud*
