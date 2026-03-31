# Rack Layout — itc-uvy — HP 10642G2 42U
**Site:** Upplands Väsby (uvy)
**Rack:** HP 10642G2 42U | U1 = bottom
**Last updated:** 2026-03-31

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
U33 ████ itc-uvy-sw-02  Cisco 3850-48P-E   Core L3               ← ports FRONT
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
U14 ████ itc-uvy-esxi-01  Dell R620 (1CCL5Y1)         ESXi 8        ✅ RACKED
U13 ████ itc-uvy-prx-01   Dell R620 (H2718X1)         → Proxmox     ✅ RACKED
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
| Compute | U12–U14 | ms-01 (U12), prx-01 (U13), esxi-01 (U14) |
| DC / expansion | U01–U11 | dc-01 tower on bottom shelf, U02–U11 free |

---

## Patch Panel Map

### PP REAR (device side)

| PP Port | Device | Device Port | Colour | Status |
|---------|--------|-------------|--------|--------|
| Port 01 | itc-uvy-ms-01 | NIC1 | Green | ✅ |
| Port 02 | itc-uvy-esxi-01 | NIC1 | Green | ✅ |
| Port 03 | itc-uvy-prx-01 | NIC1 | Green | ✅ |
| Port 04 | itc-uvy-dc-01 | LAN1 | Green | ✅ |
| Port 05 | itc-uvy-esxi-01 | NIC2 (mgmt) | Green | ⏳ |
| Port 06 | Reserved | — | — | — |
| Port 07–12 | Reserved | — | — | — |
| Port 13 | itc-uvy-dc-01 | LAN2/iDRAC | Blue | ✅ |
| Port 14 | itc-uvy-esxi-01 | iDRAC | Blue | ✅ |
| Port 15 | itc-uvy-prx-01 | iDRAC | Blue | ✅ |
| Port 16 | itc-uvy-ms-01 | iLO | Blue | ✅ |
| Port 17 | PAW T470s | enp0s31f6 | — | ✅ |
| Port 18–20 | Reserved | — | — | — |
| Port 21 | itc-uvy-rtr-01 (891F) | GE0 | White | ✅ |
| Port 22 | itc-uvy-sw-01 (3560) | GE9 | White | ✅ |
| Port 23–24 | Reserved | — | — | — |

### PP FRONT (switch side)

| PP Port | Switch | Switch Port | Colour | Status |
|---------|--------|-------------|--------|--------|
| Port 01 | 3850 | Gi1/0/3 | White | ✅ |
| Port 02 | 3850 | Gi1/0/4 | White | ✅ |
| Port 03 | 3850 | Gi1/0/5 | White | ✅ |
| Port 04 | 3850 | Gi1/0/6 | White | ✅ |
| Port 05 | 3850 | Gi1/0/7 | White | ⏳ |
| Port 06 | Reserved | — | — | — |
| Port 07–12 | Reserved | — | — | — |
| Port 13 | 3560 | GE1 | Blue | ✅ |
| Port 14 | 3560 | GE2 | Blue | ✅ |
| Port 15 | 3560 | GE3 | Blue | ✅ |
| Port 16 | 3560 | GE4 | Blue | ✅ |
| Port 17 | 3560 | GE5 | Blue | ✅ |
| Port 18–20 | Reserved | — | — | — |
| Port 21 | 3850 | Gi1/0/1 | White | ✅ |
| Port 22 | 3850 | Gi1/0/2 | White | ✅ |
| Port 23–24 | Reserved | — | — | — |

---

## Front Cabling Diagram

```
U36  }
U35  }  891F            ← ports REAR — no front cabling
U34     (free)
     │
U33  ████ 3850 (ports FRONT)
          Gi1/0/1 ──[W]──→ PP Port 21   (→ 891F GE0 via PP rear)
          Gi1/0/2 ──[W]──→ PP Port 22   (→ 3560 GE9 via PP rear)
          Gi1/0/3 ──[W]──→ PP Port 01   (server data → ms-01 NIC1)
          Gi1/0/4 ──[W]──→ PP Port 02   (server data → esxi-01 NIC1)
          Gi1/0/5 ──[W]──→ PP Port 03   (server data → prx-01 NIC1)
          Gi1/0/6 ──[W]──→ PP Port 04   (server data → dc-01 LAN1)
          Gi1/0/7 ──[W]──→ PP Port 05   (ESXi mgmt → esxi-01 NIC2) ⏳
          Gi1/0/8 ──[W]──→ PP Port 06   (reserved)
     │
U32  ████ PATCH PANEL (Digitus 24-port)
          ┌─ Ports 01–06  ← [W] from 3850 / servers rear
          ├─ Ports 07–12  ← reserved
          ├─ Ports 13–17  ← [B] from 3560 / servers OOB rear
          ├─ Ports 18–20  ← reserved
          ├─ Port  21     ← [W] 891F GE0 rear / 3850 Gi1/0/1 front
          ├─ Port  22     ← [W] 3560 GE9 rear / 3850 Gi1/0/2 front
          └─ Ports 23–24  ← reserved
     │
U31  }
U30  }  3560-CG (ports FRONT)
          GE1 ──[B]──→ PP Port 13  (iDRAC itc-uvy-dc-01)
          GE2 ──[B]──→ PP Port 14  (iDRAC itc-uvy-esxi-01)
          GE3 ──[B]──→ PP Port 15  (iDRAC itc-uvy-prx-01)
          GE4 ──[B]──→ PP Port 16  (iLO itc-uvy-ms-01)
          GE5 ──[B]──→ PP Port 17  (PAW T470s)
          GE9 ──[W]──→ PP Port 22  (uplink → 3850 Gi1/0/2 via PP)
```

---

## Rear Cabling Diagram

```
U36  }
U35  }  891F (ports REAR)
          GE0 ──[W]──→ PP Port 21 rear   (→ 3850 Gi1/0/1 front)
          GE8 ─────────→ TP-Link unmanaged (ISP/WAN — outside rack)
          PWR ──────────→ 19" power strip
U34     (free)
U33  ████ 3850   PWR → 19" power strip  ✅ Fan ×3 OK  PSU ×2 ✅
U32  ████ PP     cable routing bar ✅
U31  }
U30  }  3560-CG  PWR → 19" power strip
          GE9 ──[W]──→ PP Port 22 rear   (→ 3850 Gi1/0/2 front)
│
│    RIGHT channel (front view) — data + OOB bundles travel U12→U32
│    LEFT channel (front view)  — power → HP PDUs ✅
│
U15     ← airflow gap
U14  ████ esxi-01  → [G] NIC1 → PP02 | [B] iDRAC → PP14 | PSU×2 → PDU
U13  ████ prx-01   → [G] NIC1 → PP03 | [B] iDRAC → PP15 | PSU×2 → PDU
U12  ████ ms-01    → [G] NIC1 → PP01 | [B] iLO   → PP16 | PSU×2 → PDU
│
U01  ──── dc-01    → [G] LAN1 → PP04 | [B] LAN2  → PP13 | PSU → PDU
```

---

## Cable Inventory & Status

| Colour | Length | Purpose | VLAN | Status |
|--------|--------|---------|------|--------|
| White | 0.25m | 3850/3560 → PP front | — | ✅ |
| White | 1m | PP21 → 3850 Gi1/0/1 | — | ✅ |
| Green | 5m | Server data rear runs | VLAN 30 | ⏳ order |
| Blue | 5m | Server OOB rear runs | VLAN 10 | ⏳ order |
| Red | 0.25m | vMotion — reserved | VLAN 30 | ✅ in hand |
| Violet | 0.25m | Storage — reserved | VLAN 40 | ✅ in hand |
| Panduit Cat6 | mixed | Temporary rear runs | — | ✅ in use |
| Schuko power | 2m | Network devices → strip | — | ✅ |
| C19 → Schuko | TBC | PDU → wall | — | ✅ |

---

## Key IP Reference

| Device | Hostname | Mgmt IP (VLAN 10) | Primary IP | U pos |
|--------|----------|-------------------|------------|-------|
| Dell T330 | itc-uvy-dc-01 | 10.0.10.6 (iDRAC) | 10.0.20.2 | U01 |
| Dell R620 | itc-uvy-esxi-01 | 10.0.10.4 (iDRAC) | — | U14 |
| Dell R620 | itc-uvy-prx-01 | 10.0.10.3 (iDRAC) | — | U13 |
| HP DL360 Gen9 | itc-uvy-ms-01 | 10.0.10.5 (iLO) | — | U12 |
| Cisco 891F | itc-uvy-rtr-01 | 10.0.10.1 | — | U35–36 |
| Cisco 3560-CG | itc-uvy-sw-01 | 10.0.10.11 | — | U30–31 |
| Cisco 3850-48P-E | itc-uvy-sw-02 | 10.0.10.12 | — | U33 |
| PAW T470s | — | 10.0.10.21 | — | — |

---

## Pending / Parked

- ⏳ Green 5m × 4 — server data rear runs (permanent, replace Panduit)
- ⏳ Blue 5m × 5 — server OOB rear runs (permanent, replace Panduit)
- ⏳ dc-01 domain join + DNS verification
- ⏳ ms-01 domain join + Hyper-V role
- ⏳ prx-01 — wipe Cisco CML, install Proxmox
- ⏳ esxi-01 NIC2 mgmt → PP05 → 3850 Gi1/0/7 (when ready)
- ✅ 3850 fan module replaced — all 3 fans OK
- ✅ 3850 redundant PSU installed — PSU ×2 OK
- ✅ Dell R620 rails installed — esxi-01 U14, prx-01 U13
- ✅ Vertical HP PDUs — installed left side
- ✅ C19 → Schuko cables — PDUs connected to wall
- ✅ All network devices powered and configured
- 🔔 dc-01 virtualisation (Phase 2)
- 🔔 Optical lines + 10GbE east-west (Phase 3)

---

## Design Decisions

- **Patch panel at U32** — single cross-connect, ALL connections via PP including uplinks
- **3850 at U33** — directly above PP, short front runs ✅
- **891F at U35–36** — rear-facing ports, routes down to PP rear like a server
- **3560 at U30–31** — front-facing OOB switch
- **esxi-01 at U14, prx-01 at U13** — physically confirmed racked position
- **RIGHT channel = data + OOB, LEFT channel = power** — from front view
- **U15 airflow gap** — intentional, do not fill
- **U34 buffer** — 19" shelf clearance between 891F and 3850

---

## Notes

- 3850: Fan 2 replaced ✅, redundant PSU added ✅, Serial FOC2341X0P1
- R620 positions confirmed: esxi-01 U14, prx-01 U13 (swapped from original plan)
- All rear cable lengths use Panduit temporarily — permanent 5m order pending
- dc-01 at U01 uses right vertical channel via top horizontal bar routing
- Rack orientation: left/right always from front of rack
