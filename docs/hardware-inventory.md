# Hardware Inventory — theITchef HomeLab
**Last updated:** 2026-03-12  
**Domain:** ad.theitchef.com | **Azure region:** Sweden Central

---

## Servers

| Hostname | Model | Serial | CPU | RAM | Storage | RAID | OOB | OS/Role |
|----------|-------|--------|-----|-----|---------|------|-----|---------|
| itc-uvy-dc-01 | Dell PowerEdge T330 | 3W0MYQ2 | E3-1220 v6 | 8GB DDR4 | 1TB SATA HDD | PERC H330 | iDRAC Basic (no web UI) | WS2016 Essentials — AD/DNS |
| itc-uvy-esxi-01 | Dell PowerEdge R620 | 1CCL5Y1 | 2× E5-2660 (32t) | **304GB DDR3** | Samsung 870 1.86TB SSD | PERC H710 Mini (512MB cache) | iDRAC Enterprise | ESXi 8 — VMware/Windows VMs |
| itc-uvy-prx-01 | Dell PowerEdge R620 | H2718X1 | 2× E5-2670 (32t) | **96GB DDR3** | Kingston 480GB SSD | PERC H310 Mini | iDRAC Enterprise | → Proxmox — Linux/k3s |
| itc-uvy-sccm-01 | HP ProLiant DL360 Gen9 | CZJ54302TB | 2× E5-2630v3 (32t) | 256GB DDR4 | Samsung 870 EVO 1TB SSD | Smart Array P440ar | iLO4 Advanced | → WS2022 DC eval — SCCM/mgmt |

### Notes
- **itc-uvy-esxi-01 (1CCL5Y1):** H710 Mini BBU confirmed working normally ✅
- **itc-uvy-prx-01 (H2718X1):** RAM reduced from 128GB → 96GB (4×16GB moved to esxi-01)
- **itc-uvy-esxi-01 (1CCL5Y1):** RAM increased from 272GB → 304GB (4×16GB received from prx-01)
- **itc-uvy-sccm-01 (CZJ54302TB):** ⚠️ Processor 1 DIMM slot 12 — faulty/warning. Reseat or replace.

### Cluster Totals
| | Before swap | After swap |
|--|-------------|------------|
| Total RAM | 664GB | 664GB |
| esxi-01 | 272GB | **304GB** |
| prx-01 | 128GB | **96GB** |
| Cores/Threads | 52C / 104T | 52C / 104T |
| SSD Storage | 3.84TB | 3.84TB |

---

## Networking

| Hostname | Model | Role | Mgmt IP | Serial |
|----------|-------|------|---------|--------|
| itc-uvy-rtr-01 | Cisco 891F ISR | Edge router / WAN / NAT | 10.0.10.1 | TBC |
| itc-uvy-sw-01 | Cisco Catalyst 3560-CG PoE | OOB management switch | 10.0.10.11 | TBC |
| itc-uvy-sw-02 | Cisco Catalyst 3850-48P-E | Core L3 switch (ordered) | 10.0.10.12 | TBC |
| — | D-Link DGS-1100-08V2 | OOB mgmt switch | TBC | — |
| wifi-01 | TP-Link Archer AX12 | Wireless / Home LAN | 192.168.0.1 | — |
| — | TP-Link TL-SG105 | ISP distribution (5-port) | — | — |

---

## OOB Management

| Device | OOB Type | IP | Username | Notes |
|--------|----------|----|----------|-------|
| itc-uvy-esxi-01 | iDRAC Enterprise | 10.0.10.4 | itchef-admin | root disabled ✅ |
| itc-uvy-prx-01 | iDRAC Enterprise | 10.0.10.3 | itchef-admin | root disabled ✅ |
| itc-uvy-sccm-01 | iLO4 Advanced | 10.0.10.5 | itchef-admin | Administrator secured ✅ |
| itc-uvy-dc-01 | iDRAC Basic | 10.0.10.6 | — | No web UI, KVM only ⚠️ |

---

## Spare / Found Hardware

| Item | Qty | Spec | Location | Notes |
|------|-----|------|----------|-------|
| SAS HDD | 3× | 300GB 10K 2.5" | Bench | Compatible with R620 (2.5" bays) |
| SAS HDD | 1× | 600GB 10K 2.5" | Bench | Compatible with R620 (2.5" bays) |
| 2.5" HDD caddy | 2× | Dell R-series | Bench | For R620 hot-swap bays |

> **Note:** Both R620s (esxi-01 and prx-01) support 2.5" SAS/SATA hot-swap drives.  
> The 4× SAS drives + 2 caddies are available for use — e.g. RAID for VM storage, dedicated vMotion, or SCCM datastore.

---

## Rack Layout (U1 = bottom)

| U | Device |
|---|--------|
| U42–U35 | Blanking panels |
| U34 | 24-port Keystone Patch Panel (Phase 2) |
| U33 | 1U Cable Manager |
| U32 | itc-uvy-rtr-01 (Cisco 891F) |
| U31 | 1U Cable Manager |
| U30 | itc-uvy-sw-02 (Cisco 3850-48P-E) |
| U29 | itc-uvy-sw-01 (Cisco 3560-CG) |
| U28 | 1U Shelf → D-Link + TP-Link 5-port |
| U27 | 1U Shelf → KVM (temporary) |
| U26–U19 | Blanking panels |
| U18 | itc-uvy-prx-01 (R620) |
| U17 | itc-uvy-esxi-01 (R620) |
| U16–U13 | Blanking panels |
| U12 | itc-uvy-sccm-01 (DL360 Gen9) |
| U11 | Blanking |
| U01–U10 | itc-uvy-dc-01 (T330 on shelf) |

---

## Pending Actions

| Priority | Item |
|----------|------|
| 🔴 | Collect YubiKey 5C NFC |
| 🔴 | Order coloured patch cables (0.25m + 0.5m) — **DONE ✅** |
| 🟡 | Configure 3850 when arrives (replace 3560 as core) |
| 🟡 | Physical rack build + cabling |
| 🟡 | Reseat/replace itc-uvy-sccm-01 DIMM slot 12 (Processor 1) |
| 🟡 | Configure D-Link DGS-1100 as OOB switch (VLAN 10) |
| 🟡 | itc-uvy-prx-01 → Proxmox install |
| 🟡 | itc-uvy-sccm-01 → WS2022 DC eval install |
| 🟡 | itc-uvy-esxi-01 → ESXi 8 update to U3 + vCenter |
| 🟡 | Rename hostnames in AD, iDRAC, iLO, Cisco configs |
| 🟡 | Await Dell R620 rack rails reply |
| 🟡 | Order velcro cable ties + cable labels |
| 🟡 | Decide role for 4× SAS drives (RAID? VM storage?) |
| ℹ️ | Azure tenant region verification (Sweden Central) |
| ℹ️ | SCCM/MECM trial (Phase 3) |
| ℹ️ | FortiGate 60F purchase decision |
