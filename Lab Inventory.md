# Hardware Inventory — itc-uvy
**Last updated:** 2026-03-31

---

## Servers

| Hostname | Model | Serial | CPU | RAM | Storage | RAID | OOB | Role | U pos | Status |
|----------|-------|--------|-----|-----|---------|------|-----|------|-------|--------|
| itc-uvy-dc-01 | Dell T330 | 3W0MYQ2 | E3-1220v6 | 8GB DDR4 | 1TB SATA | H330 | iDRAC Basic 10.0.10.6 | AD/DNS — WS2016 Essentials | U01 | ✅ |
| itc-uvy-esxi-01 | Dell R620 | 1CCL5Y1 | 2×E5-2660 32t | 304GB DDR3 | 870 EVO 1.86TB SSD | H710 Mini 512MB BBU ✅ | iDRAC Enterprise 10.0.10.4 | ESXi 8 | U14 | ✅ racked |
| itc-uvy-prx-01 | Dell R620 | H2718X1 | 2×E5-2670 32t | 96GB DDR3 | Kingston 480GB SSD | H310 Mini | iDRAC Enterprise 10.0.10.3 | → Proxmox | U13 | ✅ racked |
| itc-uvy-ms-01 | HP DL360 Gen9 | CZJ54302TB | 2×E5-2630v3 32t | 256GB DDR4 | 870 EVO 1TB SSD | P440ar | iLO4 Advanced 10.0.10.5 | WS2025 DC + Hyper-V | U12 | ✅ |

### Known Issues
- ⚠️ itc-uvy-ms-01: Processor 1 DIMM slot 12 faulty — reseat/replace
- ⚠️ itc-uvy-ms-01: P440ar BBU not yet checked
- ⚠️ itc-uvy-prx-01: H310 Mini — flash to IT mode (LSI 9211-8i) when TrueNAS planned

---

## Networking

| Hostname | Model | Serial | Role | Mgmt IP | U pos | Status |
|----------|-------|--------|------|---------|-------|--------|
| itc-uvy-rtr-01 | Cisco 891F | — | Edge/WAN/NAT | 10.0.10.1 | U35–36 | ✅ |
| itc-uvy-sw-01 | Cisco 3560-CG | — | OOB switch only | 10.0.10.11 | U30–31 | ✅ |
| itc-uvy-sw-02 | Cisco 3850-48P-E | FOC2341X0P1 | Core L3 | 10.0.10.12 | U33 | ✅ |

### 3850 Hardware Notes
- Fan 1: OK ✅
- Fan 2: Replaced ✅ (was faulty on delivery)
- Fan 3: OK ✅
- PSU 1: OK ✅
- PSU 2: OK ✅ (redundant PSU added)
- License: ipservicesk9 Permanent
- IOS XE: 16.6.7

---

## Rack & Infrastructure

| Item | Model | Serial | Location | Status |
|------|-------|--------|----------|--------|
| Rack | HP 10642G2 42U | — | Upplands Väsby | ✅ |
| PDU Left | HP Modular EO4504 | CN06380863 | Zero-U left | ✅ |
| PDU Right | HP Modular EO4504 | — | Zero-U right | ✅ |
| Patch Panel | Digitus 24-port | — | U32 | ✅ keystones installed |
| OOB switch small | D-Link DGS-1100-08V2 | — | U37–38 shelf | ⏳ config pending |
| Home AP | TP-Link Archer AX11 | — | U37–38 shelf | ✅ |

---

## PAW

| Item | Details | Status |
|------|---------|--------|
| Laptop | Lenovo T470s | ✅ |
| OS | Ubuntu 24.04 LTS + LUKS | ✅ |
| Password manager | KeePassXC | ✅ |
| MFA | YubiKey 5C NFC (primary) + 5 NFC (backup) | ✅ primary configured |
| Connection | GbE → 3560 GE5 → PP17 → VLAN 10 | ✅ |
| IP | 10.0.10.21 | ✅ |

---

## Spare Hardware

| Item | Qty | Location | Plan |
|------|-----|----------|------|
| SAS 300GB 10K 2.5" | 3× | Bench | RAID 5 on esxi-01 H710 → TrueNAS VM |
| SAS 600GB 10K 2.5" | 1× | Bench | As above |
| Dell R-series 2.5" caddies | 2× | Bench | Need 2 more for RAID 5 |
| Dell 0Y4DJC rails | 2 pairs | Installed | R620 ×2 ✅ |
