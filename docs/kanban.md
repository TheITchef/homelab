# 📋 Project Kanban — HomeLab Build

> Track progress here or mirror to GitHub Projects board.  
> Update status emoji: ⬜ Todo → 🟡 In Progress → ✅ Done

---

## ⬜ Backlog

### Consumables & Hardware
- [ ] Order Cat6 patch cables (blue/black/yellow/green/red/white)
- [ ] Order 24-port Cat6 patch panel (1U)
- [ ] Order 2x 1U D-ring cable managers
- [ ] Order blanking panels (fill all empty Us)
- [ ] Order vertical PDU ×2 (IEC C13/C14, 16A, EU)
- [ ] Order velcro cable ties
- [ ] Order cable label tape (Brother P-touch)
- [ ] Order 1U shelf for D-Link OOB switch
- [ ] Check SFP module compatibility for 3560CG uplinks

### Documentation
- [ ] Draw network topology diagram (draw.io / Excalidraw)
- [ ] Create IPAM spreadsheet
- [ ] Document final cable runs in cabling.md
- [ ] Write LinkedIn post #1 — inventory & rack plan
- [ ] Write LinkedIn post #2 — rack build complete
- [ ] Write LinkedIn post #3 — ESXi cluster live

---

## 🟡 In Progress — Phase 1: Physical Build

### Inventory
- [ ] Power on Dell R620 esxi-01 → fill inventory checklist
- [ ] Power on Dell R620 esxi-02 → fill inventory checklist
- [ ] Power on HP ProLiant mgmt-01 → fill inventory checklist
- [ ] Physical session: Dell T330 nas-01 → fill inventory checklist
- [ ] Confirm iLO tier on HP ProLiant (Standard vs Advanced)
- [ ] Update inventory.md with all server specs

### Network Devices
- [x] Cisco WS-C3560CG-8PC-S — inventoried ✅
- [x] Cisco WS-C3560CG-8PC-S — factory reset ✅
- [x] Cisco C891F-K9 — inventoried ✅
- [x] Cisco C891F-K9 — factory reset ✅
- [ ] D-Link DGS-1100-08V2 — inventory & reset
- [ ] TP-Link Archer AX12 — inventory & reset

### Rack Assembly
- [ ] Clean HP 10642G2 rack interior
- [ ] Position rack (min 60cm clearance front + rear)
- [ ] Mount patch panel U1
- [ ] Mount Cisco 891F U2
- [ ] Mount cable manager U3
- [ ] Mount Cisco 3560CG U4
- [ ] Mount cable manager U5
- [ ] Mount 1U shelf + D-Link U6
- [ ] Mount Dell R620 esxi-01 U8
- [ ] Mount Dell R620 esxi-02 U9
- [ ] Mount HP ProLiant mgmt-01 U10
- [ ] Fill empty Us with blanking panels
- [ ] Install vertical PDUs rear-mount

### Cabling
- [ ] Run and dress all power cables to PDU
- [ ] Run WAN cable (red) — ISP to 891F
- [ ] Run uplink (red) — 891F Gi8 to 3560CG Gi0/9
- [ ] Run OOB cables (blue) — all iDRAC/iLO to D-Link
- [ ] Run server data cables (yellow) — NICs to 3560CG
- [ ] Run storage cables (green) — NAS NIC to 3560CG
- [ ] Label both ends of every cable
- [ ] Test continuity on all runs

---

## ✅ Done

- [x] Equipment photographed and documented
- [x] Rack model confirmed: HP 10642G2 (42U)
- [x] GitHub repo created with folder structure
- [x] Obsidian vault created
- [x] Cisco 3560CG — console access established
- [x] Cisco 3560CG — password recovery completed
- [x] Cisco 3560CG — factory reset completed
- [x] Cisco 3560CG — inventory recorded
- [x] Cisco 891F — console access established
- [x] Cisco 891F — factory reset completed
- [x] Cisco 891F — inventory recorded
- [x] Ubuntu 24.04 installed on T470s laptop
- [x] Wi-Fi configured on T470s
- [x] Obsidian installed on T470s (AppImage)
- [x] Architecture decisions logged (ADR-001 to ADR-006)

---

## 🧪 Testing & Validation

- [ ] Access all iDRAC/iLO from VLAN 10
- [ ] Change all default OOB passwords
- [ ] Confirm 891F WAN connectivity
- [ ] Confirm inter-VLAN routing (router-on-a-stick)
- [ ] Ping test across all VLANs
- [ ] Airflow check — no hot spots
- [ ] Remote power cycle test via iDRAC Enterprise (R620s)

---

## 🚀 Phase 2 — Virtualization (Planned)

- [ ] ESXi 8.x install on esxi-01 (remote via iDRAC Enterprise)
- [ ] ESXi 8.x install on esxi-02 (remote via iDRAC Enterprise)
- [ ] ESXi install on mgmt-01
- [ ] Deploy vCenter Server Appliance (VCSA)
- [ ] Form vSphere cluster
- [ ] Configure vDS (vSphere Distributed Switch)
- [ ] Configure NFS datastore from nas-01
- [ ] Deploy pfSense/OPNsense VM
- [ ] Deploy Kali VM (pentest segment)

---

## 🌩️ Phase 3 — Infrastructure Services (Planned)

- [ ] Active Directory / DNS / DHCP
- [ ] Monitoring: Grafana + Prometheus
- [ ] Logging: Loki or ELK
- [ ] Secrets: HashiCorp Vault
- [ ] Backup strategy

---

## ☁️ Phase 4 — Hybrid Cloud (Future)

- [ ] Site-to-site VPN (IKEv2 via 891F VPN module)
- [ ] Azure Arc or AWS Outposts
- [ ] Terraform for IaC
- [ ] Ansible for configuration management
- [ ] Cloud bursting policies
