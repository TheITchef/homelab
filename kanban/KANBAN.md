---
kanban-plugin: board
---

**Last updated:** 2026-03-10

## 📥 Backlog

- [ ] 3850-48P purchase decision (before Phase 2)
- [ ] Configure D-Link DGS-1100-08V2 as OOB management switch (VLAN 10)
- [ ] DC01 LAN2 → VLAN 10 (10.0.10.2), 3560-CG GE0/6
- [ ] Check H710 BBU health on esxi-02
- [ ] Check P440ar cache/BBU on mgmt-01
- [ ] Update ESXi 8.0.0 → 8.0 Update 3
- [ ] Create draw.io / Excalidraw network topology diagram
- [ ] Set up IPAM spreadsheet (IP address management)
- [ ] Order: Cat6 patch cables (colour-coded per convention)
- [ ] Order: 24-port Cat6 patch panel (1U)
- [ ] Order: 2× 1U D-ring cable managers
- [ ] Order: Blanking panels to fill empty Us
- [ ] Order: Vertical PDU ×2 (IEC C13/C14, 16A, EU)
- [ ] Order: Velcro cable ties
- [ ] Order: Cable labels / label printer tape
- [ ] Order: 1U shelf for D-Link OOB switch
- [ ] Back up KeePass database to Google Drive
- [ ] LinkedIn post #2 — Cisco network setup
- [ ] Azure tenant — verify Sweden Central region
- [ ] SCCM/MECM trial (Phase 3 prep)

## 🔨 In Progress — Phase 1 Physical

- [ ] Wednesday: collect YubiKeys + buy TP-Link TL-SG105 (5-port GbE)
- [ ] YubiKey 5C NFC + YubiKey 5 NFC setup (MFA for admin accounts)
- [ ] Change all iDRAC/iLO default passwords
- [ ] Physical rack build — mount all devices per rack layout plan
- [ ] Run and dress all power + data cables
- [ ] Label both ends of every cable
- [ ] esxi-01 — install ESXi 8 (currently running Cisco CML)

## ✅ Done

- [x] Equipment inventory photographed and documented
- [x] Rack model confirmed: HP 10642G2 (42U)
- [x] GitHub repo created: github.com/TheITchef/homelab
- [x] Project Kanban created (Obsidian)
- [x] DC01 promoted to Domain Controller (ad.theitchef.com)
- [x] AD OU structure created (_THEITCHEF hierarchy)
- [x] AD user accounts: ioannis, itchef.admin (break-glass), 6× svc.* accounts
- [x] MotoGP grid users created in People OU (17 users, valentino.rossi = VIP 👑)
- [x] Password policies: Default Domain + ServiceAccounts-PSO
- [x] Audit policy enabled (all categories, 1GB security log)
- [x] KeePass database created (theitchef-lab.kdbx)
- [x] Cisco 891F — full config (VLANs, NAT, ACLs, SSH, NTP, DHCP)
- [x] Cisco 3560-CG — full config (VLANs, trunking, SSH, NTP, port assignments)
- [x] 891F ↔ 3560-CG trunk: up/up, all VLANs, native VLAN 999
- [x] Internet connectivity confirmed through lab (NAT overload)
- [x] DC01 migrated from home LAN (192.168.0.50) → lab VLAN 20 (10.0.20.2)
- [x] T470s PAW connected to lab: GbE → 3560-CG GE0/5 (VLAN 20)
- [x] RDP from T470s → DC01 working
- [x] DNS persistence fixed on T470s (netplan → NetworkManager)
- [x] Running configs saved to GitHub (configs/cisco/)
- [x] LinkedIn profile set up (TheITchef)
- [x] LinkedIn post #1 published (lab intro)

## 🧪 Testing & Validation

- [ ] Access all iDRAC/iLO interfaces from VLAN 10
- [ ] Confirm inter-VLAN routing (ping across all VLANs from mgmt host)
- [ ] Confirm WAN failover / ACL behaviour
- [ ] Check airflow — no hot spots, all blanking panels in place
- [ ] Document final cable runs

## 🚀 Phase 2 — Virtualization (Future)

- [ ] ESXi 8.x install on esxi-01 (currently CML — reinstall)
- [ ] ESXi 8.x already on esxi-02 — update to 8.0 U3
- [ ] Deploy vCenter Server Appliance (VCSA)
- [ ] Form vSphere cluster (esxi-01, esxi-02)
- [ ] Configure vDS (vSphere Distributed Switch)
- [ ] Configure shared storage
- [ ] Deploy monitoring stack (Grafana/Prometheus or similar)
- [ ] LinkedIn post #3 — vSphere cluster live

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false,false,false,false]}
```
%%