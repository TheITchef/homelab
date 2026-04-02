# Microsoft Virtualization Architecture — itc‑uvy  
**Last updated:** 2026‑04‑02  
**Applies to:** itc‑uvy‑ms‑01 (HP DL360 Gen9)

---

# 🎯 Purpose

This document defines the **virtualized Microsoft infrastructure architecture** running on the DL360 Gen9 Hyper‑V host.  
All Microsoft services — AD DS, DNS, Entra Connect, SQL, MECM, PKI, WSUS, File Services — are deployed as **virtual machines**, not physical roles.

This design aligns with modern enterprise practices:

- Isolation of roles  
- Snapshot and rollback capability  
- Portability between hypervisors  
- Simplified backup and DR  
- Clean security boundaries  
- Easier lifecycle management  

---

# 🧱 Hyper‑V Host Overview

**Host:** itc‑uvy‑ms‑01  
**Model:** HP DL360 Gen9  
**OS:** Windows Server 2025 Datacenter  
**Role:** Hyper‑V only (no domain roles on bare metal)

### Host Configuration

| Component | Value |
|----------|--------|
| CPU | 2× Intel Xeon E5‑2630v3 (32 threads) |
| RAM | 256GB DDR4 |
| Storage | 1TB SSD (P440ar) |
| NIC1 | VLAN 30 — Hyper‑V host management |
| NIC2 | VLAN 10 — Optional mgmt / out‑of‑band |
| iLO4 | VLAN 10 — OOB management |
| Domain Membership | Member of ad.theitchef.com (optional) |

**No roles installed except Hyper‑V.**  
No AD DS, DNS, SQL, SCCM, or Entra Connect on the host.

---

# 🖥️ Virtual Machine Architecture

All Microsoft infrastructure services run as VMs.  
This section defines the baseline VM set.

---

## 1. DC01‑VM — Primary Domain Controller

| Setting | Value |
|--------|--------|
| OS | Windows Server 2025 |
| vCPU | 2 |
| RAM | 8–12GB |
| Disk | 60GB |
| Network | VLAN 30 (SERVERS) |
| Roles | AD DS, DNS |

**Notes:**  
- First VM to be deployed  
- Becomes forest root DC  
- SYSVOL replication via DFS‑R  

---

## 2. AADC01‑VM — Entra Connect

| Setting | Value |
|--------|--------|
| OS | Windows Server 2025 |
| vCPU | 2–4 |
| RAM | 8GB |
| Disk | 60GB |
| Network | VLAN 30 |
| Roles | Entra Connect Sync |

**Notes:**  
- Syncs on‑prem AD → Entra ID  
- Supports password hash sync or pass‑through auth  

---

## 3. SQL01‑VM — SQL Server 2022

| Setting | Value |
|--------|--------|
| OS | Windows Server 2025 |
| vCPU | 4–8 |
| RAM | 16–32GB |
| Disk | 60GB OS + 100GB DB + 50GB Logs |
| Network | VLAN 30 |
| Roles | SQL Server 2022 Standard/Eval |

**Notes:**  
- Backend for MECM  
- Dedicated disks for DB + logs  

---

## 4. SCCM01‑VM — MECM / SCCM

| Setting | Value |
|--------|--------|
| OS | Windows Server 2025 |
| vCPU | 4–8 |
| RAM | 16–24GB |
| Disk | 80–120GB |
| Network | VLAN 30 |
| Roles | MECM Primary Site |

**Notes:**  
- Uses SQL01 as backend  
- Optional DP on Proxmox or ESXi later  

---

## 5. MGMT01‑VM — Admin Jump Host

| Setting | Value |
|--------|--------|
| OS | Windows Server 2025 or Windows 11 Enterprise |
| vCPU | 2 |
| RAM | 4–8GB |
| Disk | 40GB |
| Network | VLAN 30 |
| Roles | RSAT, Azure tools, admin workstation |

**Notes:**  
- Used for AD, DNS, MECM, SQL, Azure admin  
- Reduces need to log into servers directly  

---

## Optional VMs

### PKI01‑VM — ADCS  
- Enterprise CA  
- 2 vCPU / 4GB RAM  
- VLAN 30  

### WSUS01‑VM  
- 2 vCPU / 8GB RAM  
- VLAN 30  

### FS01‑VM — File Server  
- 2–4 vCPU / 8GB RAM  
- VLAN 30  

### Backup Server (Veeam CE)  
- 2–4 vCPU / 8GB RAM  
- VLAN 30  

---

# 🌐 Networking Architecture

### VLAN Placement

| VLAN | Purpose | VM Placement |
|------|----------|--------------|
| 30 | SERVERS | All Microsoft VMs |
| 10 | MGMT | Hyper‑V host mgmt + iLO |
| 40 | STORAGE | Optional future iSCSI/NFS |
| 20 | LAN | Client devices |
| 50 | DMZ | Optional external services |

### Routing

- All SVIs and routing handled by **Cisco 3850‑48P‑E**  
- Hyper‑V host and VMs use 3850 as default gateway  
- 3560‑CG is OOB‑only  

---

# 🔐 Security Model

- Hyper‑V host is **not** a domain controller  
- All domain roles isolated inside VMs  
- iLO isolated in VLAN 10  
- Admin access via MGMT01‑VM  
- Backups stored off‑host (Proxmox/TrueNAS or external disk)  

---

# 🧩 Backup & DR Strategy

### Recommended:
- Veeam Community Edition  
- Hyper‑V VM‑level backups  
- Off‑host storage (Proxmox NFS, TrueNAS, or external SSD)  
- Pre‑change snapshots for:  
  - Schema updates  
  - SQL patching  
  - MECM upgrades  
  - Entra Connect updates  

---

# 🚀 Future Expansion

- Azure Arc onboarding  
- Hybrid identity lab  
- Multi‑site AD replication (optional)  
- Failover cluster (if second Hyper‑V host added)  
- Nested virtualization for lab scenarios  

---

*Tags: #microsoft #virtualization #hyperv #homelab #architecture #entra #sccm #sql*
