# 🖥️ HomeLab — Complete Hardware Inventory

> Last updated: 2026-03-06  

> Status: ✅ Full inventory complete  

> *Tags: #homelab #inventory #phase1*

  

---

  

## Summary Table

  

| Host | Model | CPU | Cores/Threads | RAM | Storage | RAID | NIC | OOB | OS |

|------|-------|-----|---------------|-----|---------|------|-----|-----|----|

| esxi-01 | Dell R620 | 2× E5-2670 @ 2.6GHz | 16c/32t | 128GB DDR3 | 480GB SSD | H310 | 4× BCM5720 1GbE | iDRAC Enterprise | Cisco CML (expired) |

| esxi-02 | Dell R620 | 2× E5-2660 @ 2.2GHz | 16c/32t | 272GB DDR3 | 1.86TB SSD | H710 512MB | 4× Intel I350 1GbE | iDRAC Enterprise | ESXi 8.0.0 |

| mgmt-01 | HP DL360 Gen9 | 2× E5-2630v3 @ 2.4GHz | 16c/32t | 256GB DDR4 | 1TB SSD | P440ar | 4× GbE | iLO4 Advanced | WS2022 DC (expired) |

| nas-01 | Dell T330 | E3-1220 v6 @ 3.0GHz | 4c/4t | 8GB DDR4 | 1TB SATA HDD | H330 | BCM5720 1GbE | iDRAC Basic | Bare |

  

---

  

## esxi-01 — Dell PowerEdge R620

  

| Field | Value |

|-------|-------|

| Service Tag | H2718X1 |

| Express Service Code | 37138047589 |

| BIOS | 2.9.0 |

| iDRAC Firmware | 2.65.65.65 |

| iDRAC License | Enterprise ✅ |

| iDRAC MAC | E0:DB:55:1F:E2:9A |

| iDRAC IP | 192.168.0.120 (DHCP — assign static) |

| Board S/N | CN7475132D0572 |

| Current Hostname | MINWINPC |

  

### CPU

| Socket | Model | Cores | Threads | Base | Turbo | L3 |

|--------|-------|-------|---------|------|-------|----|

| 1 | Intel Xeon E5-2670 | 8 | 16 | 2.6GHz | 3.3GHz | 20MB |

| 2 | Intel Xeon E5-2670 | 8 | 16 | 2.6GHz | 3.3GHz | 20MB |

  

**Total: 16 cores / 32 threads**

  

### Memory — 128GB DDR3 (12/24 slots)

| Slot | Size | Speed | Vendor |

|------|------|-------|--------|

| A1 | 8GB | 1333MHz | Hynix |

| A2 | 8GB | 1333MHz | Hynix |

| A5 | 8GB | 1333MHz | Samsung |

| A6 | 8GB | 1333MHz | Samsung |

| A9 | 8GB | 1333MHz | Hynix |

| A10 | 8GB | 1333MHz | Samsung |

| B3 | 8GB | 1333MHz | Hynix |

| B4 | 16GB | 1600→1333MHz | Samsung |

| B7 | 8GB | 1333MHz | Hynix |

| B8 | 16GB | 1600→1333MHz | Samsung |

| B11 | 16GB | 1600→1333MHz | Samsung |

| B12 | 16GB | 1600→1333MHz | Samsung |

  

> ⚠️ Mixed 8GB/16GB config — running at 1333MHz. 12 slots free for expansion up to 384GB.

  

### Storage

| Slot | Model | Capacity | Type | Status |

|------|-------|----------|------|--------|

| Bay 0 | Kingston SA400S | 480GB | SATA SSD | ⚠️ Non-Dell flag (benign) |

  

### RAID Controller

| Field | Value |

|-------|-------|

| Model | PERC H310 Mini |

| Cache | None |

| BBU | None |

| Firmware | 20.13.3-0001 |

  

### Network

| Port | Chip | MAC | Speed |

|------|------|-----|-------|

| NIC 1 | Broadcom BCM5720 | 90:B1:1C:3D:C2:B1 | 1GbE |

| NIC 2 | Broadcom BCM5720 | 90:B1:1C:3D:C2:B2 | 1GbE |

| NIC 3 | Broadcom BCM5720 | 90:B1:1C:3D:C2:B3 | 1GbE |

| NIC 4 | Broadcom BCM5720 | 90:B1:1C:3D:C2:B4 | 1GbE |

| iDRAC | Dedicated | E0:DB:55:1F:E2:9A | 1GbE |

  

### Power

| PSU | Model | Wattage | Connector | Status |

|-----|-------|---------|-----------|--------|

| PSU 1 | Dell 750W Redundant (Delta) | 750W | C13 | ✅ OK |

| PSU 2 | Dell 750W Redundant (Delta) | 750W | C13 | ⚠️ Not cabled |

  

### Action Items

- [ ] 🔴 Clear non-Dell drive alert in iDRAC Storage

- [ ] 🟡 Connect PSU2 to PDU-B when rack is cabled

- [ ] 🟡 Change iDRAC default password

- [ ] 🟡 Rename hostname to `esxi-01`

- [ ] 🟡 Decision: keep CML or repurpose as ESXi node

- [ ] ℹ️ Consider PERC H710 upgrade (~€20 used) for VM workloads

  

---

  

## esxi-02 — Dell PowerEdge R620

  

| Field | Value |

|-------|-------|

| Service Tag | 1CCL5Y1 |

| Express Service Code | 2923519321 |

| BIOS | 2.9.0 |

| iDRAC Firmware | 2.65.65.65 |

| iDRAC License | Enterprise ✅ |

| iDRAC MAC | 74:86:7A:CE:68:B2 |

| iDRAC IP | 192.168.0.120 (DHCP — assign static) |

| Board S/N | CN7475134C0415 |

| Current Hostname | *(blank)* |

  

### CPU

| Socket | Model | Cores | Threads | Base | Turbo | L3 |

|--------|-------|-------|---------|------|-------|----|

| 1 | Intel Xeon E5-2660 | 8 | 16 | 2.2GHz | 3.0GHz | 20MB |

| 2 | Intel Xeon E5-2660 | 8 | 16 | 2.2GHz | 3.0GHz | 20MB |

  

**Total: 16 cores / 32 threads**

  

### Memory — 272GB DDR3 (24/24 slots)

| Slot | Size | Speed | Vendor |

|------|------|-------|--------|

| A1–A4 | 16GB ×4 | 1600→1333MHz | Samsung |

| A5 | 8GB | 1333MHz | Hynix |

| A6 | 8GB | 1333MHz | Hynix |

| A7 | 16GB | 1600→1333MHz | Samsung |

| A8 | 8GB | 1333MHz | Hynix |

| A9 | 8GB | 1333MHz | Hynix |

| A10 | 8GB | 1333MHz | Hynix |

| A11 | 8GB | 1333MHz | Samsung |

| A12 | 8GB | 1333MHz | Hynix |

| B1–B4 | 16GB ×4 | 1600→1333MHz | Samsung |

| B5 | 8GB | 1333MHz | Samsung |

| B6 | 16GB | 1600→1333MHz | Samsung |

| B7 | 8GB | 1333MHz | Hynix |

| B8 | 8GB | 1333MHz | Hynix |

| B9 | 8GB | 1600→1333MHz | Samsung |

| B10 | 8GB | 1600→1333MHz | Samsung |

| B11 | 8GB | 1333MHz | Hynix |

| B12 | 8GB | 1333MHz | Hynix |

  

> ⚠️ Mixed config — all slots populated, running at 1333MHz. Could reach 384GB @ 1600MHz with matched 16GB DIMMs.

  

### Storage

| Slot | Model | Capacity | Type | Status |

|------|-------|----------|------|--------|

| Bay 0 | Samsung SSD 870 | 1.86TB | SATA SSD | ✅ Online |

  

### RAID Controller

| Field | Value |

|-------|-------|

| Model | PERC H710 Mini ✅ |

| Cache | 512MB ✅ |

| Encryption | Capable |

| Firmware | 21.3.5-0002 |

  

### Network

| Port | Chip | MAC | Speed |

|------|------|-----|-------|

| NIC 1 | Intel I350-t | B8:CA:3A:5F:9C:7C | 1GbE |

| NIC 2 | Intel I350-t | B8:CA:3A:5F:9C:7D | 1GbE |

| NIC 3 | Intel I350-t | B8:CA:3A:5F:9C:7E | 1GbE |

| NIC 4 | Intel I350-t | B8:CA:3A:5F:9C:7F | 1GbE |

| iDRAC | Dedicated | 74:86:7A:CE:68:B2 | 1GbE |

  

### Power

| PSU | Model | Wattage | Connector | Status |

|-----|-------|---------|-----------|--------|

| PSU 1 | Dell 750W Redundant (Delta) | 750W | C13 | ⚠️ Monitor — failed Jul 2025 |

| PSU 2 | Dell 750W Redundant (Delta) | 750W | C13 | ✅ OK |

  

### Action Items

- [ ] 🔴 Check H710 BBU health → iDRAC → Storage → Battery

- [ ] 🟡 Monitor PSU1 — recurring fault history

- [ ] 🟡 Change iDRAC default password

- [ ] 🟡 Rename hostname to `esxi-02`

- [ ] 🟡 Update ESXi 8.0.0 → 8.0 Update 3 (do all hosts together)

- [ ] ℹ️ RAM optimisation — replace 8GB Hynix DIMMs with 16GB Samsung for full 384GB @ 1600MHz

  

---

  

## mgmt-01 — HP ProLiant DL360 Gen9

  

| Field | Value |

|-------|-------|

| Serial Number | CZJ54302TB |

| iLO Firmware | iLO 4 Advanced ✅ |

| iLO IP | 192.168.0.130 (DHCP — assign static) |

| iLO DNS | ILOCZJ54302TB |

| iLO Default User | Administrator |

| Current OS | Windows Server 2022 Datacenter (expired) |

  

### CPU

| Socket | Model | Cores | Threads | Base | Turbo | L3 |

|--------|-------|-------|---------|------|-------|----|

| 1 | Intel Xeon E5-2630 v3 | 8 | 16 | 2.4GHz | 3.2GHz | 20MB |

| 2 | Intel Xeon E5-2630 v3 | 8 | 16 | 2.4GHz | 3.2GHz | 20MB |

  

**Total: 16 cores / 32 threads**

  

### Memory — 256GB DDR4 (8 slots)

| Config | Size | Speed | Vendor | ECC |

|--------|------|-------|--------|-----|

| 8× DIMM | 32GB each | 1866MHz | HPE/Hynix | Advanced ECC ✅ |

  

> ✅ Only DDR4 server in the lab. Fully matched config — no mixed DIMM issues.

  

### Storage

| Slot | Model | Capacity | Type | Status |

|------|-------|----------|------|--------|

| Bay 0 | Samsung 870 EVO | 1TB | SATA SSD | ✅ |

  

### RAID Controller

| Field | Value |

|-------|-------|

| Model | HPE Smart Array P440ar |

| Cache | TBC — check iLO |

| BBU | TBC — check iLO |

  

### Network

| Port | Speed | Count |

|------|-------|-------|

| Integrated GbE | 1GbE | 4× |

  

### Power

| PSU | Wattage | Connector | Status |

|-----|---------|-----------|--------|

| PSU 1 | 500W Flex | C13 | ✅ OK |

| PSU 2 | 500W Flex | C13 | ✅ OK |

  

### Action Items

- [ ] 🔴 Change iLO default password

- [ ] 🟡 Check P440ar cache and BBU status in iLO

- [ ] 🟡 Assign static iLO IP on VLAN 10

- [ ] 🟡 Fix iLO session timeout → Administration → Security → 60 min

- [ ] 🟡 Decision: keep WS2022 or repurpose (vCenter? Ubuntu?)

  

---

  

## nas-01 — Dell PowerEdge T330

  

| Field | Value |

|-------|-------|

| Service Tag | 3W0MYQ2 |

| iDRAC License | Basic |

| iDRAC IP | 192.168.0.120 (DHCP — assign static) |

| Current OS | Bare metal |

  

### CPU

| Model | Cores | Threads | Base |

|-------|-------|---------|------|

| Intel Xeon E3-1220 v6 | 4 | 4 | 3.0GHz |

  

### Memory

| Size | Speed | Vendor | Type |

|------|-------|--------|------|

| 8GB | 2400MHz | Hynix | DDR4 ECC |

  

> ⚠️ Single DIMM — no memory redundancy. Expandable to 64GB max (4 slots).

  

### Storage

| Bay | Model | Capacity | Type | Status |

|-----|-------|----------|------|--------|

| Bay 0 | Dell/Seagate | 1TB | SATA HDD | ✅ |

| Bay 1–3 | — | Empty | LFF 3.5" | Available |

| Bay 4–7 | — | Empty | LFF 3.5" | Backplane supports 8× |

  

> 💡 4 free LFF bays — ideal for adding cheap NAS drives (4TB–8TB SATA HDDs).

  

### RAID Controller

| Field | Value |

|-------|-------|

| Model | PERC H330 |

| Cache | None |

| BBU | None |

  

### Network

| Port | Chip | Speed |

|------|------|-------|

| NIC 1 | Broadcom BCM5720 | 1GbE |

| iDRAC | Basic — dedicated | 1GbE |

  

### Power

| PSU | Wattage | Redundancy |

|-----|---------|------------|

| Single | 495W | None |

  

### Action Items

- [ ] 🔴 Physical console required for OS install (iDRAC Basic — no KVM)

- [ ] 🟡 Change iDRAC default password

- [ ] 🟡 Install OS — TrueNAS or Ubuntu Server

- [ ] 🟡 Add drives to empty bays for NFS/SMB storage

- [ ] ℹ️ RAM upgrade — 8GB is minimal, consider 2× 16GB for NAS OS headroom

  

---

  

## 🌐 Network Devices

  

| Device | Model | IP | Credentials | Firmware | Notes |

|--------|-------|----|-------------|----------|-------|

| router-01 | Cisco 891F ISR | TBC | Default | TBC | Change pw |

| sw-core-01 | Cisco Catalyst 3560-CG PoE | TBC | Default | TBC | Change pw |

| sw-mgmt-01 | D-Link DGS-1100-08V2 | TBC | Default | 1.00.003 | Change pw |

| wifi-01 | TP-Link Archer AX12 | TBC | Default | TBC | Change pw, rename SSID |

  

---

  

## 📊 Cluster Totals

  

| Resource | Total |

|----------|-------|

| Physical servers | 4 |

| Total CPU cores | 52 cores / 104 threads |

| Total RAM | **664 GB** |

| Total SSD storage | 3.84 TB |

| Total HDD storage | 1 TB |

| 1GbE ports | 17 |

  

---

  

## ⚠️ Known Issues Log

  

| Host | Issue | Severity | Status |

|------|-------|----------|--------|

| esxi-01 | Non-Dell drive alert (Kingston) | 🟡 Low | Benign — clear alert |

| esxi-01 | PSU2 not cabled | 🟡 Low | Fix during rack cabling |

| esxi-01 | CMOS battery replaced | ✅ | Resolved |

| esxi-01 | PERC H310 — no cache | ℹ️ Info | By design |

| esxi-02 | PSU1 fan/input fault history Jul 2025 | 🟡 Monitor | Currently OK |

| esxi-02 | H710 BBU health unknown | 🟡 Check | Pending verification |

| esxi-02 | Mixed RAM at 1333MHz | ℹ️ Info | Functional |

| mgmt-01 | iLO session timeout too short | 🟡 Low | Fix in settings |

| mgmt-01 | P440ar cache/BBU unknown | 🟡 Check | Pending verification |

| nas-01 | 8GB RAM minimal for NAS OS | ℹ️ Info | Upgrade optional |

| All | Default OOB passwords not changed | 🔴 Security | Do immediately |

  

---

  

*Tags: #homelab #inventory #hardware #phase1 #complete*