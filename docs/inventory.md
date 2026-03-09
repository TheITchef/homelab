# 🖥️ Hardware & Network Inventory

> Last updated: 2026-03-08
> Status: ✅ Complete — all devices inventoried
> Tags: #homelab #inventory #phase1

---

## Summary Table

| Host | Model | CPU | Cores | RAM | Storage | Role |
|------|-------|-----|-------|-----|---------|------|
| DC01 | Dell T330 | E3-1220 v6 | 4c/4t | 8GB DDR4 | 1TB HDD | AD DS / DNS / DHCP |
| esxi-01 | Dell R620 | 2x E5-2670 | 16c/32t | 128GB DDR3 | 480GB SSD | VMware ESXi |
| esxi-02 | Dell R620 | 2x E5-2660 | 16c/32t | 272GB DDR3 | 1.86TB SSD | VMware ESXi (primary) |
| mgmt-01 | HP DL360 G9 | 2x E5-2630v3 | 16c/32t | 256GB DDR4 | 1TB SSD | vCenter / Management |

**Cluster total: 52 cores / 104 threads / 664GB RAM / 3.84TB SSD / 1TB HDD**

---

## Rack

| Field | Value |
|-------|-------|
| Model | HP 10642G2 |
| Size | 42U |
| Status | In place |
| PDU | Vertical PDU x2 (planned) |
| Tower | Dell T330 DC01 beside rack |

---

## DC01 — Dell PowerEdge T330

| Field | Value |
|-------|-------|
| Role | Domain Controller / DNS / DHCP |
| Service Tag | 3W0MYQ2 |
| OS | Windows Server 2016 Essentials (OEM) |
| AD Domain | ad.theitchef.com |
| NetBIOS | THEITCHEF |
| iDRAC License | Basic (no remote KVM) |
| iDRAC IP | 192.168.0.120 (temp) → 10.0.10.2 |
| Server IP | 192.168.0.50 (temp) → 10.0.20.2 |

### CPU
| Model | Cores | Threads | Base |
|-------|-------|---------|------|
| Intel Xeon E3-1220 v6 | 4 | 4 | 3.0GHz |

### Memory
| Size | Speed | Type | Slots Used |
|------|-------|------|------------|
| 8GB | 2400MHz | DDR4 ECC UDIMM | 1/4 |

> Single DIMM — no redundancy. Sufficient for DC role. Max 64GB (4 slots).

### Storage
| Bay | Model | Capacity | Type |
|-----|-------|----------|------|
| Bay 0 | Dell/Seagate | 1TB | SATA HDD v6 |
| Bay 1-7 | Empty | — | LFF 3.5" available |

### RAID / Network / Power
| Component | Detail |
|-----------|--------|
| RAID | PERC H330 — no cache |
| NIC | Broadcom BCM5720 1GbE |
| PSU | Single 495W (no redundancy) |

### Status
- [x] AD DS promoted — ad.theitchef.com
- [x] OU structure created
- [x] Password policy hardened
- [x] Audit policy enabled
- [ ] iDRAC password — change default
- [ ] Static IP assignment — VLAN 10/20
- [ ] Service account password issue — investigate

---

## esxi-01 — Dell PowerEdge R620

| Field | Value |
|-------|-------|
| Role | VMware ESXi (decision pending — currently Cisco CML) |
| Service Tag | H2718X1 |
| Board S/N | CN7475132D0572 |
| BIOS | 2.9.0 |
| iDRAC Firmware | 2.65.65.65 |
| iDRAC License | Enterprise |
| iDRAC MAC | E0:DB:55:1F:E2:9A |
| iDRAC IP | 192.168.0.120 (temp) → 10.0.10.3 |
| Current OS | Cisco CML (expired) |

### CPU
2x Intel Xeon E5-2670 — 8 cores / 16 threads each — 2.6GHz base / 3.3GHz turbo / 20MB L3
Total: 16 cores / 32 threads

### Memory — 128GB DDR3 (12/24 slots)
Mixed 8GB/16GB Samsung/Hynix config at 1333MHz. 12 slots free — expandable to 384GB.

### Storage / RAID / Network / Power
| Component | Detail |
|-----------|--------|
| Storage | Kingston SA400S 480GB SATA SSD |
| RAID | PERC H310 Mini — no cache, no BBU |
| NIC 1-4 | Broadcom BCM5720 — MACs: 90:B1:1C:3D:C2:B1 to :B4 |
| iDRAC NIC | E0:DB:55:1F:E2:9A |
| PSU 1 | Dell 750W Redundant (Delta) — OK |
| PSU 2 | Dell 750W Redundant (Delta) — not cabled |

### Status
- [ ] Clear non-Dell drive alert (Kingston SSD — benign)
- [ ] Change iDRAC default password
- [ ] Connect PSU2 during rack cabling
- [ ] Decision: keep CML or repurpose as ESXi
- [ ] Consider PERC H710 upgrade (~€20)

---

## esxi-02 — Dell PowerEdge R620

| Field | Value |
|-------|-------|
| Role | VMware ESXi — primary compute |
| Service Tag | 1CCL5Y1 |
| Board S/N | CN7475134C0415 |
| BIOS | 2.9.0 |
| iDRAC Firmware | 2.65.65.65 |
| iDRAC License | Enterprise |
| iDRAC MAC | 74:86:7A:CE:68:B2 |
| iDRAC IP | 192.168.0.120 (temp) → 10.0.10.4 |
| Current OS | ESXi 8.0.0 (needs update) |

### CPU
2x Intel Xeon E5-2660 — 8 cores / 16 threads each — 2.2GHz base / 3.0GHz turbo / 20MB L3
Total: 16 cores / 32 threads

### Memory — 272GB DDR3 (24/24 slots — fully populated)
Mixed Samsung/Hynix config at 1333MHz. Could reach 384GB with matched 16GB Samsung DIMMs.

### Storage / RAID / Network / Power
| Component | Detail |
|-----------|--------|
| Storage | Samsung SSD 870 — 1.86TB SATA |
| RAID | PERC H710 Mini — 512MB cache — check BBU |
| NIC 1-4 | Intel I350-t — MACs: B8:CA:3A:5F:9C:7C to :7F |
| iDRAC NIC | 74:86:7A:CE:68:B2 |
| PSU 1 | Dell 750W Redundant — MONITOR (failed Jul 2025) |
| PSU 2 | Dell 750W Redundant — OK |

> Intel I350 NICs preferred for VMware — better driver support than Broadcom.

### Status
- [ ] Check H710 BBU health
- [ ] Change iDRAC default password
- [ ] Monitor PSU1 — fault history Jul 2025
- [ ] Update ESXi 8.0.0 → 8.0 Update 3

---

## mgmt-01 — HP ProLiant DL360 Gen9

| Field | Value |
|-------|-------|
| Role | vCenter Server / Management plane |
| Serial Number | CZJ54302TB |
| iLO | iLO 4 Advanced |
| iLO IP | 192.168.0.130 (temp) → 10.0.10.5 |
| iLO DNS | ILOCZJ54302TB |
| Current OS | Windows Server 2022 DC (expired) |

### CPU
2x Intel Xeon E5-2630 v3 — 8 cores / 16 threads each — 2.4GHz base / 3.2GHz turbo
Total: 16 cores / 32 threads

### Memory — 256GB DDR4 (8/8 slots — fully populated)
8x HPE 32GB RDIMMs at 1866MHz. Advanced ECC. Only DDR4 server in the lab.
Note: HPE RDIMMs — NOT compatible with T330 (requires UDIMM).

### Storage / RAID / Network / Power
| Component | Detail |
|-----------|--------|
| Storage | Samsung 870 EVO 1TB SATA SSD |
| RAID | HPE Smart Array P440ar — cache/BBU TBC |
| NIC | 4x Integrated GbE |
| PSU 1 | 500W Flex — OK |
| PSU 2 | 500W Flex — OK |

### Status
- [ ] Change iLO default password
- [ ] Check P440ar cache and BBU
- [ ] Fix iLO session timeout (60 min)
- [ ] Assign static iLO IP — 10.0.10.5
- [ ] Decision: vCenter or repurpose

---

## Network Devices

### Cisco C891F-K9 — router-01

| Field | Value |
|-------|-------|
| Role | WAN / Edge router |
| Serial | FCZ2213E0EW |
| IOS | 15.4(3)M3 |
| License | advipservices — Permanent |
| RAM | 488MB |
| Flash | 250MB CompactFlash |
| Interfaces | 1x FE WAN, 9x GbE LAN, 1x SFP |
| Mgmt IP | TBC → 10.0.10.10 |
| Status | Reset — clean config |

### Cisco WS-C3560CG-8PC-S — sw-core-01

| Field | Value |
|-------|-------|
| Role | L3 Core switch / VLAN routing |
| Serial | FOC1820Y6HW |
| MAC | 38:1C:1A:F8:9F:80 |
| IOS | 12.2(55)EX2 |
| License | ipbase — Permanent |
| Ports | 8x GbE PoE + 2x GbE SFP/RJ45 combo |
| Mgmt IP | TBC → 10.0.10.11 |
| Status | Reset — clean config |

### D-Link DGS-1100-08V2 — sw-mgmt-01

| Field | Value |
|-------|-------|
| Role | OOB management switch |
| MAC | BC:22:28:04:4D:90 |
| Firmware | 1.00.003 |
| Ports | 8x GbE |
| Management | Web UI only (Smart Managed) |
| Mgmt IP | TBC → 10.0.10.12 |

### TP-Link Archer AX12 — wifi-01

| Field | Value |
|-------|-------|
| Role | Wireless access |
| Standard | Wi-Fi 6 AX1500 |
| SSID | 666 (custom) |
| Target VLAN | 99 |
| Status | Operational |

---

## Admin Workstation — PAW

| Field | Value |
|-------|-------|
| Device | Lenovo ThinkPad T470s |
| OS | Ubuntu 24.04 LTS |
| Encryption | LUKS full disk encryption |
| Role | Privileged Access Workstation |
| MFA | YubiKey 5C NFC + YubiKey 5 NFC (ordered) |
| Tools | Remmina, KeePass2, git, gh CLI |

---

## Known Issues

| Host | Issue | Severity | Status |
|------|-------|----------|--------|
| DC01 | Service account password policy issue | Investigate | Pending |
| esxi-01 | Non-Dell drive alert (Kingston) | Low | Clear in iDRAC |
| esxi-01 | PSU2 not cabled | Low | Fix during rack build |
| esxi-02 | PSU1 fault history Jul 2025 | Monitor | Currently OK |
| esxi-02 | H710 BBU health unknown | Check | Pending |
| esxi-02 | Mixed RAM at 1333MHz | Info | Functional |
| mgmt-01 | iLO session timeout short | Low | Fix in settings |
| mgmt-01 | P440ar cache/BBU unknown | Check | Pending |
| All | Default OOB passwords not changed | High | Do immediately |

---

*Last updated: 2026-03-08*
