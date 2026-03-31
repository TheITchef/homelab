# KANBAN — itc-uvy Homelab
**Last updated:** 2026-03-31

---

## ✅ DONE

- [x] Rack installed and positioned
- [x] HP PDUs installed (zero-U, left side)
- [x] C19→Schuko cables — PDUs connected to wall
- [x] 19" shelves installed (2U each)
- [x] Vertical cable channels identified (right=data, left=power)
- [x] Cisco 891F configured — hostname, VLANs, SSH, hardened
- [x] Cisco 3560-CG configured — hostname, VLANs, SSH, OOB ports
- [x] Cisco 3850-48P-E received, configured — hostname, VLANs, SSH
- [x] 3850 Fan 2 replaced ✅
- [x] 3850 redundant PSU installed ✅
- [x] Dell R620 rails received and installed (×2)
- [x] esxi-01 racked at U14 ✅
- [x] prx-01 racked at U13 ✅
- [x] ms-01 (DL360) at U12 ✅
- [x] dc-01 (T330) on shelf at U01 ✅
- [x] Patch panel installed at U32 with 30× keystone couplers
- [x] PP rear connections: Ports 01, 02, 03, 04, 13, 14, 15, 16, 17, 21, 22
- [x] PP front connections: Ports 01, 02, 03, 04, 13, 14, 15, 16, 17, 21, 22
- [x] 891F→3850 trunk up, all VLANs active
- [x] 3850→3560 trunk up, native VLAN mismatch resolved
- [x] PAW SSH config for all network devices
- [x] ms-01 WS2025 Datacenter installed
- [x] ms-01 renamed to itc-uvy-ms-01
- [x] PAW connected via PP17 → 3560 GE5 → VLAN 10
- [x] YubiKey 5C NFC FIDO2 PIN configured
- [x] KeePassXC installed on PAW

---

## 🔄 IN PROGRESS

- [ ] Hostname renames — all devices (runbook ready)
  - [ ] DC01 → itc-uvy-dc-01 (netdom)
  - [ ] esxi-02 → itc-uvy-esxi-01
  - [ ] esxi-01 → itc-uvy-prx-01
  - [ ] mgmt-01 → itc-uvy-ms-01 (done via fresh install)
- [ ] dc-01 power up and DNS verification
- [ ] ms-01 domain join to ad.theitchef.com
- [ ] ms-01 Hyper-V role installation
- [ ] YubiKey KeePassXC integration (TOTP)
- [ ] esxi-01 and prx-01 iDRAC verification via PP

---

## 📋 TODO — Phase 1

- [ ] D-Link DGS-1100 config — assign 10.0.10.10, VLAN 10
- [ ] ms-01 BBU check via iLO (P440ar)
- [ ] ms-01 DIMM slot 12 reseat/replace
- [ ] prx-01 — wipe Cisco CML, install Proxmox
- [ ] esxi-01 NIC2 mgmt → PP05 → 3850 Gi1/0/7
- [ ] KeePass backup to Google Drive
- [ ] Order permanent rear cables (Green 5m ×4, Blue 5m ×5)
- [ ] Replace Panduit temporary runs with permanent coloured cables
- [ ] DNS records for all devices on dc-01
- [ ] Save all Cisco configs to GitHub configs/cisco/
- [ ] Update port-mapping.pdf
- [ ] 3850 config backup to GitHub

---

## 🔔 PARKED / FUTURE

- [ ] TrueNAS VM on esxi-01 — NFS over VLAN 40 (needs 2 more SAS caddies)
- [ ] H310 flash to IT mode on prx-01 (LSI 9211-8i compatible)
- [ ] SAS drives RAID 5 on esxi-01 H710 (needs 2 more caddies)
- [ ] dc-01 virtualisation → Phase 2 (frees U01–U11)
- [ ] Hyper-V VMs on ms-01: sccm-01, wsus-01, ca-01, mgmt-01
- [ ] Azure hybrid cloud integration
- [ ] Optical lines + 10GbE east-west — Phase 3
- [ ] C3850-NM-2-10G module + R620 mezz NICs — Phase 3
- [ ] Second patch panel at U35 — next wave
- [ ] Rack rails R620 ×2 — ✅ installed
- [ ] HP ROK WS2025 Datacenter key for ms-01

---

## 📦 PENDING DELIVERIES

- [ ] Green Cat6 5m ×4 (server data permanent)
- [ ] Blue Cat6 5m ×5 (server OOB permanent)

---

## 📊 PROGRESS

| Phase | Progress |
|-------|---------|
| Phase 1 — Physical infrastructure | ~75% |
| Phase 1 — Network config | ~60% |
| Phase 1 — Server config | ~30% |
| Overall | ~45% |
