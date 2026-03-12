# Kanban — theITchef HomeLab
**Last updated:** 2026-03-12

---

## ✅ Done

- [x] AD DS promoted on itc-uvy-dc-01
- [x] AD hardening (tiered admin, fine-grained password policy, audit policy)
- [x] KeePass2 set up on T470s PAW
- [x] GitHub repo created (TheITchef/homelab)
- [x] LinkedIn post #1 published (lab intro)
- [x] iDRAC hardened on itc-uvy-prx-01 + itc-uvy-esxi-01
- [x] iLO4 hardened on itc-uvy-sccm-01
- [x] DC01 LAN2 connected to VLAN 10 (10.0.10.2)
- [x] Cisco 891F fully configured (itc-uvy-rtr-01)
- [x] Cisco 3560-CG fully configured (itc-uvy-sw-01, demoted to OOB)
- [x] PAW T470s connected — GbE → 3560-CG, DNS → DC01
- [x] SSH shortcut configured for 3560-CG on T470s
- [x] Rack diagram created (docs/rack-diagram.html)
- [x] Port mapping documented
- [x] VLAN design finalised
- [x] Naming convention confirmed: itc-uvy-[role]-[number]
- [x] Cable colour scheme finalised + ordered (Amazon.se)
- [x] Cisco 3850-48P-E ordered (renewtech.se, 1055 SEK)
- [x] Digitus patch panels ordered ×2
- [x] 1U cable managers ordered ×2 (Temu)
- [x] Blanking panels ×20 ordered (Temu)
- [x] iDRAC XML exports parsed for both R620s
- [x] RAM redistribution plan created
- [x] RAM swap completed — itc-uvy-esxi-01: 304GB, itc-uvy-prx-01: 96GB ✅
- [x] H710 Mini BBU confirmed healthy on itc-uvy-esxi-01 ✅
- [x] YubiKey 5 NFC backup found
- [x] TP-Link TL-SG105 bought

---

## 🔴 Urgent / Next

- [ ] Collect YubiKey 5C NFC
- [ ] Rename hostnames in AD, iDRAC/iLO, Cisco device configs
- [ ] Order velcro cable ties + cable labels

---

## 🟡 In Progress / Upcoming

- [ ] Configure 3850-48P-E as core L3 when arrives
- [ ] Physical rack build + cabling
- [ ] Configure D-Link DGS-1100 as OOB switch (VLAN 10)
- [ ] Reseat/replace itc-uvy-sccm-01 DIMM slot 12 (Processor 1)
- [ ] Proxmox install on itc-uvy-prx-01
- [ ] WS2022 DC eval install on itc-uvy-sccm-01
- [ ] ESXi 8 update to U3 + vCenter deploy on itc-uvy-esxi-01
- [ ] Check P440ar cache/BBU on itc-uvy-sccm-01
- [ ] Await Dell R620 rack rails reply from seller
- [ ] Back up KeePass to Google Drive
- [ ] LinkedIn post #2 publish (when rack built)
- [ ] Decide role for 4× SAS 2.5" drives (found on bench) — RAID? VM storage? Spare?

---

## ℹ️ Backlog / Phase 3

- [ ] Azure tenant region verification (Sweden Central)
- [ ] SCCM/MECM trial
- [ ] FortiGate 60F purchase decision
- [ ] 305m Cat6 solid core box (buy from Elfa/Dustin/Inet.se — Phase 2 cabling)
- [ ] vMotion network design + test
- [ ] Azure Arc onboarding
- [ ] IaC — Terraform / Ansible groundwork
