# 🏠 HomeLab — Project Hub

> **Status:** 🟡 In Progress  
> **Phase:** 1 — Physical Build, Networking, Virtualized AD  
> **Repo:** `github.com/TheITchef/homelab`  
> **Last updated:** 2026‑04‑02

---

## 🗂️ Quick Links

- [[homelab-kanban]] — Kanban Board  
- [[homelab-cabling]] — Structured Cabling Guide  
- `docs/vlan-design.md` — Network Topology & VLANs  
- `docs/rack-diagram.html` — Visual Rack Diagram  
- `lessons-learned/` — Engineering journal  

---

# 🖥️ Server Roles (2026 Architecture Revision)

The 2026 rebuild introduces a major shift:  
**All Microsoft infrastructure services are now virtualized on the DL360 Hyper‑V host.**

| Host | Model | RAM | Role (Revised) | Track |
|------|-------|-----|----------------|-------|
| itc‑uvy‑ms‑01 | HP DL360 Gen9 | 256GB | **Hyper‑V host (all Microsoft infra virtualized)** | Microsoft |
| itc‑uvy‑dc‑01 | Dell T330 | 8GB | **Legacy — to be demoted** | Microsoft |
| itc‑uvy‑esxi‑01 | Dell R620 (H2718X1) | 96GB | Proxmox — Linux VMs, k3s, SRE/DevOps stack | SRE / DevOps |
| itc‑uvy‑esxi‑02 | Dell R620 (1CCL5Y1) | 304GB | ESXi 8 — VMware + Windows VMs | Microsoft / VMware |

This replaces the old table where the T330 was listed as “AD/DNS — permanent” and the DL360 as “Windows Server DC — SCCM, SQL, management plane”.  


---

# 🌐 Three Tracks

### 🔵 Microsoft Track
- Hyper‑V virtualization (DL360)  
- Virtualized AD DS, DNS, Entra Connect  
- SQL Server + MECM (SCCM)  
- Azure Arc  
- Hybrid identity (Phase 4)

### 🟢 SRE / DevOps Track
- Proxmox on esxi‑01  
- k3s Kubernetes cluster  
- Prometheus + Grafana + Alertmanager  
- Loki or ELK logging  
- Terraform + Ansible (IaC)  
- GitLab CI/CD  
- Docker → Kubernetes progression

### 🔴 Networking Track
- Cisco 891F (edge, WAN, NAT) — **active**  
- Cisco 3850‑48P‑E — **active L3 core**  
- Cisco 3560‑CG — **OOB‑only**  
- FortiGate 60F (optional future NGFW)

The previous version listed the 3850 as “ordered” — this is now corrected.  


---

# 🧱 Equipment Inventory (Revised)

| Host | Model | CPU | RAM | Storage | Role |
|------|-------|-----|-----|---------|------|
| itc‑uvy‑ms‑01 | HP DL360 Gen9 | 2×E5‑2630v3 | 256GB | 1TB SSD | **Hyper‑V host** |
| itc‑uvy‑esxi‑01 | Dell R620 | 2×E5‑2670 | 96GB | 480GB SSD | Proxmox |
| itc‑uvy‑esxi‑02 | Dell R620 | 2×E5‑2660 | 304GB | 1.86TB SSD | ESXi 8 |
| itc‑uvy‑dc‑01 | Dell T330 | E3‑1220v6 | 8GB | 1TB HDD | **Legacy — to be demoted** |

This replaces the old table where the DL360 was “SCCM/mgmt” and the T330 was active AD/DNS.  


---

# 🌐 VLAN Design

*(unchanged — still valid)*

| VLAN | Name | Subnet | Purpose |
|------|------|--------|---------|
| 10 | MGMT | 10.0.10.0/24 | iDRAC, iLO, switch mgmt |
| 20 | LAN | 10.0.20.0/24 | Workstations |
| 30 | SERVERS | 10.0.30.0/24 | VM production |
| 40 | STORAGE | 10.0.40.0/24 | NFS/iSCSI |
| 50 | DMZ | 10.0.50.0/24 | Internet‑facing |
| 99 | WIFI | 10.0.99.0/24 | Wireless |
| 999 | NATIVE | — | Hardened native VLAN |

---

# 📐 Rack Layout (Updated)

Reflects the actual rack state from `rack-layout.md`, including:

- DL360 at U12  
- R620s at U13–U14  
- 3850 at U33 (active core)  
- 3560 at U30–31 (OOB)  
- T330 at U01 (legacy)  



---

# 🔗 Phase Roadmap (Revised 2026)

Phase 1: Physical Build & Foundation        ← IN PROGRESS
├─ Cisco 891F + 3560-CG configured  ✓
├─ Cisco 3850 installed as L3 core  ✓
├─ DL360 installed with WS2025      ✓
├─ Hyper-V role enabled             ✓
├─ T330 marked for decommission     ✓
└─ Structured cabling (ongoing)

Phase 2: Virtualization Layer
├─ Deploy DC01-VM (AD DS + DNS)
├─ Migrate AD from T330 → VM
├─ Deploy AADC01-VM (Entra Connect)
├─ Deploy SQL01-VM + SCCM01-VM
└─ vCenter on esxi-02

Phase 3: Infrastructure Services
├─ PKI, WSUS, File Server (optional)
├─ Monitoring stack (Grafana/Prometheus)
└─ Backup (Veeam CE)

Phase 4: Hybrid Cloud
├─ Azure Arc
├─ Entra Connect Sync
├─ S2S VPN (891F)
└─ Optional FortiGate NGFW

Phase 5: Advanced
├─ Service mesh
├─ ML/AI workloads
└─ Multi-cloud experiments
Code


---

# 📝 Architecture Decisions Log (Updated)

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026‑04‑02 | DL360 becomes Hyper‑V host only | Enables full virtualization of Microsoft infra |
| 2026‑04‑02 | T330 demoted to legacy | WS2016 Essentials incompatible with Entra Connect |
| 2026‑04‑02 | All Microsoft services virtualized | Isolation, snapshots, portability |
| 2026‑04‑02 | 3850 becomes active L3 core | Enterprise‑grade routing, SVIs, east‑west traffic |
| 2026‑03‑10 | esxi‑02 → ESXi 8 | Strongest compute node |
| 2026‑03‑10 | esxi‑01 → Proxmox | Linux-native SRE stack |
| 2026‑03‑08 | 3560-CG demoted to OOB | 3850 replaces it as core |

This replaces the old decisions where the DL360 was planned as a physical DC/SCCM server.  


---

*Tags: #homelab #infrastructure #virtualization #hyperv #cisco #microsoft #sccm #entra #hybridcloud*