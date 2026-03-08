# 🔍 Hardware Inventory Checklist

> Fill this in during a physical inspection session + iDRAC/iLO web UI login.  
> Takes ~15 min per server. Do T330 first (no remote KVM after).  
> *Tags: #homelab #inventory #phase1*

---

## How to Get the Info

| Info | Where to find it |
|------|-----------------|
| Model / Service Tag | iDRAC → System Summary **or** physical label rear of unit |
| CPU | iDRAC → System Summary → Processor |
| RAM | iDRAC → System Summary → Memory |
| Drives | iDRAC → Storage → Physical Disks |
| NICs | iDRAC → System Summary → Network Devices |
| iDRAC version/tier | iDRAC → Overview → iDRAC Information |
| PSU count & wattage | iDRAC → Power → Power Supplies **or** physical label |
| Firmware versions | iDRAC → Overview → Firmware Versions |

---

## 🖥️ esxi-01 — Dell PowerEdge R620

### Identity
- [ ] **Model confirmed:** `___________________________`
- [ ] **Service Tag:** `___________________________`
- [ ] **iDRAC IP assigned:** `10.0.10.___`
- [ ] **iDRAC tier:** `[ ] Basic  [ ] Express  [x] Enterprise`

### CPU
- [ ] **Socket count:** `___`
- [ ] **CPU model:** `___________________________`
- [ ] **Cores per CPU:** `___`  **Total cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`
- [ ] **Config (e.g. 8×16GB):** `___________________________`

### Storage
| Slot | Capacity | Interface | RPM / Type | Status |
|------|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

- [ ] **RAID controller model:** `___________________________`
- [ ] **RAID controller cache:** `___ MB  [ ] Battery backed  [ ] Capacitor  [ ] None`

### Network
| Port | Label | Speed | MAC | Notes |
|------|-------|-------|-----|-------|
| NIC1 | | | | |
| NIC2 | | | | |
| NIC3 | | | | |
| NIC4 | | | | |
| iDRAC | | 1GbE | | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage each:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C19`

### Firmware
- [ ] **iDRAC firmware version:** `___________________________`
- [ ] **BIOS version:** `___________________________`
- [ ] **PERC firmware version:** `___________________________`

### Notes
```

```

---

## 🖥️ esxi-02 — Dell PowerEdge R620

### Identity
- [ ] **Model confirmed:** `___________________________`
- [ ] **Service Tag:** `___________________________`
- [ ] **iDRAC IP assigned:** `10.0.10.___`
- [ ] **iDRAC tier:** `[ ] Basic  [ ] Express  [x] Enterprise`

### CPU
- [ ] **Socket count:** `___`
- [ ] **CPU model:** `___________________________`
- [ ] **Cores per CPU:** `___`  **Total cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`
- [ ] **Config (e.g. 8×16GB):** `___________________________`

### Storage
| Slot | Capacity | Interface | RPM / Type | Status |
|------|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

- [ ] **RAID controller model:** `___________________________`
- [ ] **RAID controller cache:** `___ MB  [ ] Battery backed  [ ] Capacitor  [ ] None`

### Network
| Port | Label | Speed | MAC | Notes |
|------|-------|-------|-----|-------|
| NIC1 | | | | |
| NIC2 | | | | |
| NIC3 | | | | |
| NIC4 | | | | |
| iDRAC | | 1GbE | | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage each:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C19`

### Firmware
- [ ] **iDRAC firmware version:** `___________________________`
- [ ] **BIOS version:** `___________________________`
- [ ] **PERC firmware version:** `___________________________`

### Notes
```

```

---

## 🖥️ esxi-03 — Dell PowerEdge PI-ESXI-50 *(model TBC)*

### Identity
- [ ] **Model confirmed:** `___________________________`
- [ ] **Service Tag:** `___________________________`
- [ ] **iDRAC IP assigned:** `10.0.10.___`
- [ ] **iDRAC tier:** `[ ] Basic  [ ] Express  [ ] Enterprise`

### CPU
- [ ] **Socket count:** `___`
- [ ] **CPU model:** `___________________________`
- [ ] **Cores per CPU:** `___`  **Total cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`
- [ ] **Config:** `___________________________`

### Storage
| Slot | Capacity | Interface | RPM / Type | Status |
|------|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

- [ ] **RAID controller model:** `___________________________`
- [ ] **RAID controller cache:** `___ MB  [ ] Battery backed  [ ] Capacitor  [ ] None`

### Network
| Port | Label | Speed | MAC | Notes |
|------|-------|-------|-----|-------|
| NIC1 | | | | |
| NIC2 | | | | |
| NIC3 | | | | |
| NIC4 | | | | |
| iDRAC | | 1GbE | | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage each:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C19`

### Firmware
- [ ] **iDRAC firmware version:** `___________________________`
- [ ] **BIOS version:** `___________________________`
- [ ] **PERC firmware version:** `___________________________`

### Notes
```

```

---

## 🖥️ esxi-04 — Dell PowerEdge PI-ESXI-50 *(model TBC)*

### Identity
- [ ] **Model confirmed:** `___________________________`
- [ ] **Service Tag:** `___________________________`
- [ ] **iDRAC IP assigned:** `10.0.10.___`
- [ ] **iDRAC tier:** `[ ] Basic  [ ] Express  [ ] Enterprise`

### CPU
- [ ] **Socket count:** `___`
- [ ] **CPU model:** `___________________________`
- [ ] **Cores per CPU:** `___`  **Total cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`
- [ ] **Config:** `___________________________`

### Storage
| Slot | Capacity | Interface | RPM / Type | Status |
|------|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

- [ ] **RAID controller model:** `___________________________`
- [ ] **RAID controller cache:** `___ MB  [ ] Battery backed  [ ] Capacitor  [ ] None`

### Network
| Port | Label | Speed | MAC | Notes |
|------|-------|-------|-----|-------|
| NIC1 | | | | |
| NIC2 | | | | |
| NIC3 | | | | |
| NIC4 | | | | |
| iDRAC | | 1GbE | | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage each:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C19`

### Firmware
- [ ] **iDRAC firmware version:** `___________________________`
- [ ] **BIOS version:** `___________________________`
- [ ] **PERC firmware version:** `___________________________`

### Notes
```

```

---

## 🖥️ mgmt-01 — HP ProLiant (S/N CZJ54302TB)

### Identity
- [ ] **Model confirmed:** `___________________________`
- [ ] **Serial Number:** `CZJ54302TB`
- [ ] **iLO IP assigned:** `10.0.10.___`
- [ ] **iLO tier:** `[ ] Standard  [ ] Advanced  [ ] Advanced Premium`

### CPU
- [ ] **Socket count:** `___`
- [ ] **CPU model:** `___________________________`
- [ ] **Cores per CPU:** `___`  **Total cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`

### Storage
| Slot | Capacity | Interface | RPM / Type | Status |
|------|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

- [ ] **RAID controller model:** `___________________________`

### Network
| Port | Label | Speed | MAC | Notes |
|------|-------|-------|-----|-------|
| NIC1 | | | | |
| NIC2 | | | | |
| iLO | | 1GbE | | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage each:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C19`

### Firmware
- [ ] **iLO firmware version:** `___________________________`
- [ ] **BIOS / System ROM version:** `___________________________`

### Notes
```

```

---

## 🖥️ nas-01 — Dell PowerEdge T330

> ⚠️ iDRAC Basic — no remote KVM. **Complete this section physically on-site.**

### Identity
- [ ] **Model confirmed:** `PowerEdge T330`
- [ ] **Service Tag:** `3W0MYQ2`
- [ ] **iDRAC IP assigned:** `10.0.10.___`
- [ ] **iDRAC tier:** `[x] Basic`

### CPU
- [ ] **CPU model:** `___________________________`
- [ ] **Cores:** `___`
- [ ] **Clock speed:** `___ GHz`

### Memory
- [ ] **Total RAM:** `___ GB`
- [ ] **Speed:** `___ MHz`  **Type:** `[ ] DDR3  [ ] DDR4`
- [ ] **Slots used / total:** `___ / ___`

### Storage
| Bay | Capacity | Interface | RPM / Type | Status |
|-----|----------|-----------|------------|--------|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| Internal | | | SSD/HDD | OS drive |

- [ ] **RAID controller model:** `___________________________`
- [ ] **Optical drive present:** `[ ] Yes  [ ] No`

### Network
| Port  | Speed | MAC | Notes     |
| ----- | ----- | --- | --------- |
| NIC1  |       |     |           |
| NIC2  |       |     |           |
| iDRAC | 1GbE  |     | dedicated |

### Power
- [ ] **PSU count:** `[ ] 1  [ ] 2`
- [ ] **PSU wattage:** `___ W`
- [ ] **Connector type:** `[ ] C13  [ ] C14`

### Firmware
- [ ] **iDRAC firmware version:** `___________________________`
- [ ] **BIOS version:** `___________________________`

### Planned OS
- [ ] `[ ] Ubuntu Server 22.04  [ ] TrueNAS  [ ] Windows Server  [ ] Other: ___`

### Notes
```

```

---

## 🌐 Network Devices

### Cisco 891F ISR
- [ ] **IOS version:** `___________________________`
- [ ] **RAM:** `___ MB`
- [ ] **Flash:** `___ MB`
- [ ] **WAN IP (ISP):** `___________________________`
- [ ] **Serial number:** `___________________________`

### Cisco Catalyst 3560-CG PoE
- [ ] **IOS version:** `___________________________`
- [ ] **Total ports:** `___`
- [ ] **PoE budget:** `___ W`
- [ ] **Serial number:** `___________________________`
- [ ] **SFP slots:** `___`  **SFP modules installed:** `[ ] Yes  [ ] No`

### D-Link DGS-1100-08V2
- [ ] **Firmware version:** `1.00.003` *(confirmed from label)*
- [ ] **MAC:** `BC:22:28:04:4D:90` *(confirmed from label)*
- [ ] **Management IP assigned:** `10.0.10.___`

### TP-Link Archer AX12
- [ ] **Firmware version:** `___________________________`
- [ ] **LAN IP:** `___________________________`
- [ ] **SSID 2.4GHz:** `TP-Link_E16C` *(confirmed from label)*
- [ ] **SSID 5GHz:** `TP-Link_E16C_5G` *(confirmed from label)*
- [ ] **Wi-Fi password changed:** `[ ] Yes  [ ] No`

---

## ✅ Session Completion

- [ ] All servers powered on and POST completed without errors
- [ ] All iDRAC/iLO web UIs accessible from laptop
- [ ] All default passwords changed and saved to password manager
- [ ] All fields in this document filled
- [ ] Photos taken of drive bays, rear I/O, and any anomalies
- [ ] T330 physical console session completed
- [ ] Checklist committed to GitHub repo

---

*Tags: #homelab #inventory #hardware #phase1*
