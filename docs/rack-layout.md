# Rack Layout — itc-uvy — HP 10642G2 42U
**Site:** Upplands Väsby (uvy)
**Rack:** HP 10642G2 42U | U1 = bottom
**Last updated:** 2026-03-16

---

## Current Layout

```
U42
U41
U40
U39
U38 ──── Shelf    }
U37 ────          }  TP-Link Archer AX11 + D-Link DGS-1100-08V2  OOB mgmt / home AP
U36 ──── Shelf    }
U35 ────          }  itc-uvy-rtr-01  Cisco 891F   Edge/WAN/NAT   ← ports REAR
U34                  (free — buffer U between 891F shelf and 3850)
U33 ████ itc-uvy-sw-02  Cisco 3850-48P-E   Core L3               ← ports FRONT [ARRIVING]
U32 ████ Patch Panel    Digitus 24-port     ← cable routing bar behind ✅
U31 ──── Shelf    }
U30 ────          }  itc-uvy-sw-01  Cisco 3560-CG  OOB switch     ← ports FRONT
U29 ──── Shelf    }
U28 ────          }  (free — spare shelf)
U27
U26
U25
U24
U23
U22                  ← cable corridor / future expansion
U21
U20
U19
U18
U17 ──── Shelf    }
U16 ────          }  Telescopic shelf — Screen / Keyboard / Mouse (console)
U15                  ← airflow gap (thermal separation — do not fill)
U14 ████ itc-uvy-prx-01   Dell R620 (H2718X1)         → Proxmox     [PENDING RAILS]
U13 ████ itc-uvy-esxi-01  Dell R620 (1CCL5Y1)         ESXi 8        [PENDING RAILS]
U12 ████ itc-uvy-ms-01    HP DL360 Gen9 (CZJ54302TB)  WS2025 DC + Hyper-V
U11
U10
U09
U08
U07
U06
U05
U04
U03
U02
U01 ──── Shelf         itc-uvy-dc-01 (Dell T330)      AD/DNS — WS2016 Essentials
```

---

## Zone Summary

| Zone | U positions | Contents |
|------|------------|----------|
| Accessories | U37–U38 | TP-Link AP + D-Link OOB shelf |
| Router | U35–U36 | 891F on shelf — ports REAR |
| Buffer | U34 | Free — 19" shelf clearance |
| Core switch | U33 | 3850 rack mounted — ports FRONT |
| Patch Panel | U32 | Digitus 24-port — single cross-connect |
| OOB switch | U30–U31 | 3560-CG on shelf — ports FRONT |
| Free shelf | U28–U29 | Spare |
| Cable corridor | U18–U27 | Intentional space — rear dressing, future expansion |
| Console | U16–U17 | Telescopic shelf — screen/keyboard/mouse |
| Airflow gap | U15 | Thermal separation — do not fill |
| Compute | U12–U14 | ms-01, esxi-01, prx-01 |
| DC / expansion | U01–U11 | dc-01 tower on bottom shelf, U02–U11 free |

---

## Front Cabling Diagram

```
U36  }
U35  }  891F            ← ports REAR — no front cabling
U34     (free)
     │
U33  ████ 3850 (ports FRONT)
          Gi1/0/1 ──[W]0.25m──→ Patch Panel Port 21   (→ 891F GE0 via PP rear)
          Gi1/0/2 ──[W]0.25m──→ Patch Panel Port 22   (→ 3560 GE9 via PP rear)
          Gi1/0/3 ──[W]0.25m──→ Patch Panel Port 01   (server data → ms-01)
          Gi1/0/4 ──[W]0.25m──→ Patch Panel Port 02   (server data → esxi-01)
          Gi1/0/5 ──[W]0.25m──→ Patch Panel Port 03   (server data → prx-01)
          Gi1/0/6 ──[W]0.25m──→ Patch Panel Port 04   (server data → dc-01)
          Gi1/0/7 ──[W]0.25m──→ Patch Panel Port 05   (ESXi mgmt → esxi-01 NIC2)
          Gi1/0/8 ──[W]0.25m──→ Patch Panel Port 06   (reserved)
     │
U32  ████ PATCH PANEL (Digitus 24-port)
          ┌─ Ports 01–06  ← [W] from 3850       server data (front) / servers (rear)
          ├─ Ports 07–12  ← reserved             future data
          ├─ Ports 13–17  ← [B] from 3560        OOB management
          ├─ Ports 18–20  ← reserved             future OOB
          ├─ Port  21     ← [W] from 3850        → 891F GE0 (rear) routed uplink
          ├─ Port  22     ← [W] from 3850        → 3560 GE9 (rear) OOB uplink
          ├─ Port  23     ← reserved             future uplink
          └─ Port  24     ← reserved             future uplink
     │
U31  }
U30  }  3560-CG (ports FRONT)
          GE1 ──[B]0.25m──→ Patch Panel Port 13  (iDRAC itc-uvy-dc-01)
          GE2 ──[B]0.25m──→ Patch Panel Port 14  (iDRAC itc-uvy-esxi-01)
          GE3 ──[B]0.25m──→ Patch Panel Port 15  (iDRAC itc-uvy-prx-01)
          GE4 ──[B]0.25m──→ Patch Panel Port 16  (iLO itc-uvy-ms-01)
          GE5 ──[B]0.25m──→ Patch Panel Port 17  (D-Link OOB mgmt)
          GE9 ──[W]0.25m──→ Patch Panel Port 22  (uplink → 3850 Gi1/0/2 via PP)
```

---

## Rear Cabling Diagram

```
U36  }
U35  }  891F (ports REAR)
          GE0 ──[W]TBC──→ Patch Panel Port 21 rear  (→ 3850 Gi1/0/1 front)
          GE8 ──────────→ TP-Link unmanaged switch   (ISP/WAN split — outside rack)
          PWR ──[Schuko]─→ 19" power strip           (power)
U34     (free)
     │
U33  ████ 3850             ← PWR → 19" power strip
U32  ████ Patch Panel      ← cable routing bar ✅
                              rear ports terminate:
                              - 891F uplink (Port 21)
                              - 3560 uplink (Port 22)
                              - all server data runs (Ports 01–06)
                              - all server OOB runs (Ports 13–17)
U31  }
U30  }  3560-CG            ← PWR → 19" power strip
          GE9 ──[W]──→ Patch Panel Port 22 rear     (uplink → 3850 via PP)
     │
│    ← cable corridor
│       [W] data bundles travel RIGHT rear upright U12 → U32
│       [B] OOB bundles travel LEFT rear upright U12 → U32
│       power cables LEFT side → vertical HP PDUs ✅
│
U15     ← airflow gap
U14  ████ prx-01    → [W][B] exit rear → upright → PP rear routing bar → PP rear ports
U13  ████ esxi-01   → [W][W][R][V][B] exit rear → upright → PP rear routing bar → PP rear ports
U12  ████ ms-01     → [W][B] exit rear → upright → PP rear routing bar → PP rear ports
│
│    Power: Schuko → vertical HP PDUs (left side) ✅
│
U01  ──── dc-01     → [W][B] longest run — MEASURE U01→U32 before ordering
```

---

## Cable Inventory & Status

| Colour | Length | Purpose | VLAN | In hand | Status |
|--------|--------|---------|------|---------|--------|
| White | 0.25m | 3850 → PP front / 3560 → PP front | — | 20× | ✅ now correct length |
| White | 0.5m | Server data upruns rear | — | 20× | ✅ |
| Green | 0.5m | Spare / future uplinks | — | 5× | ✅ |
| Blue | 0.5m | OOB mgmt 3560 → PP | VLAN 10 | 10× | 📦 incoming |
| Blue | 0.25m | OOB mgmt 3560 → PP (now correct length) | VLAN 10 | 5× | ✅ |
| Magenta | 0.25m | Reserved — future short server data | VLAN 30 | 5× | ✅ |
| Red | 0.25m | vMotion esxi-01 NIC3 → PP TBC | VLAN 30 | 5× | ✅ |
| Violet | 0.25m | Storage esxi-01 NIC4 → PP TBC | VLAN 40 | 5× | ✅ |
| Panduit Cat6 | 1/1.5/2/3m | Temporary rear runs | — | mixed | ✅ |
| Schuko power | 2m | Network devices → 19" power strip | — | 5× | 📦 incoming |

---

## Key IP Reference

| Device | Hostname | Mgmt IP (VLAN 10) | Primary IP |
|--------|----------|-------------------|------------|
| Dell T330 | itc-uvy-dc-01 | 10.0.10.6 (iDRAC) | 10.0.20.2 |
| Dell R620 | itc-uvy-esxi-01 | 10.0.10.4 (iDRAC) | — |
| Dell R620 | itc-uvy-prx-01 | 10.0.10.3 (iDRAC) | — |
| HP DL360 Gen9 | itc-uvy-ms-01 | 10.0.10.5 (iLO) | — |
| Cisco 891F | itc-uvy-rtr-01 | 10.0.10.1 | — |
| Cisco 3560-CG | itc-uvy-sw-01 | 10.0.10.11 | — |
| Cisco 3850-48P-E | itc-uvy-sw-02 | 10.0.10.12 | — |

---

## Pending / Parked

- 📦 itc-uvy-sw-02 (3850) — ordered, arriving
- 📦 2× Dell 0Y4DJC Type A7 sliding rails — ordered (one pair per R620)
- 📦 2× 1U ring panel cable managers — ordered
- 📦 1× Schuko 19" power strip (network devices) — ordered
- 📦 Velcro roll 10m × 2cm — ordered
- 📦 Snap-in D-rings ×20 — ordered
- 📦 10× Blue Cat6 0.5m — ordered
- 📦 5× Schuko power cables 2m — ordered
- 📦 30× Cat6 feedthrough keystone couplers — ordered
- ⏳ Rear cable lengths — measure all server runs U12–U01 → U32 before ordering
- ✅ Vertical HP PDUs — installed, zero-U left side of rack
- ✅ Coloured patch cables in hand
- ✅ 19" shelves installed (2U each)
- 🔔 dc-01 virtualisation (Phase 2) — will free U01–U11 entirely
- 🔔 Optical lines + 10GbE east-west (Phase 3)

---

## Design Decisions

- **Patch panel at U32** — true single cross-connect point. ALL connections route through PP, including device-to-device uplinks. No direct device-to-device cables
- **3850 at U33** — directly above PP, 0.25m white cables now sufficient for all front runs ✅
- **891F at U35–U36** — ports face REAR, cables exit back and route down to PP rear. Behaves like a server from a cabling perspective
- **3560 at U30–U31** — ports face FRONT, 0.25m blue cables now sufficient for all OOB runs ✅
- **U34 free** — buffer between 891F shelf bottom and 3850 top (19" shelf clearance requirement)
- **Cable routing bar behind PP (U32)** — captures all rear server runs and 891F rear runs cleanly before termination
- **Left = PDU side** — convention always from front of rack
- **U15 airflow gap** — intentional, do not fill
- **Rear cable highway U18–U27** — intentional empty space

---

## Notes

- 891F ports face REAR — treated as server-side device for cabling purposes
- 3850 and 3560 ports face FRONT — all runs 0.25m to PP ✅ short cables now work
- 19" shelves occupy 2U each and create 1U clearance above/below — factor into placement
- All server rear cable lengths TBC — use Panduit temporarily, measure, supplemental order
- dc-01 at U01 has longest runs (U01→U32) — measure carefully before ordering
- Rack orientation: left/right always from front of rack
