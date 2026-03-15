# Rack Layout — itc-uvy — HP 10642G2 42U
**Site:** Upplands Väsby (uvy)
**Rack:** HP 10642G2 42U | U1 = bottom
**Last updated:** 2026-03-15

---

## Current Layout

```
U34 ░░░░ Cable Manager       ← dresses server upruns before patch panel
U33 ████ itc-uvy-sw-02       Cisco 3850-48P-E            VLAN trunk / core L3 (rack mounted) [ARRIVING]
U32 ████ Patch Panel          Digitus 24-port
U31 ──── Shelf    }
U30 ────          }           itc-uvy-rtr-01  Cisco 891F  Edge / WAN / NAT
U29 ──── Shelf    }
U28 ────          }           itc-uvy-sw-01  Cisco 3560-CG  OOB switch only
U27 ──── Shelf                (free — spare 19" shelf)
U26
U25
U24
U23
U22                           ← cable corridor / future expansion
U21
U20
U19
U18
U17 ──── Shelf    }
U16 ────          }           Telescopic shelf — Screen / Keyboard / Mouse (console)
U15                           ← airflow gap (thermal separation — do not fill)
U14 ████ itc-uvy-prx-01       Dell R620 (H2718X1)         → Proxmox     [PENDING RAILS]
U13 ████ itc-uvy-esxi-01      Dell R620 (1CCL5Y1)         ESXi 8        [PENDING RAILS]
U12 ████ itc-uvy-sccm-01      HP DL360 Gen9 (CZJ54302TB)  → WS2022 SCCM
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
U01 ──── Shelf                itc-uvy-dc-01 (Dell T330)   AD/DNS — WS2016 Essentials
```

---

## Zone Summary

| Zone | U positions | Contents |
|------|------------|----------|
| Networking | U28–U34 | Switches, router, patch panel, cable manager |
| Accessories | U27 | Free shelf |
| Cable corridor | U18–U26 | Intentional space — rear cable dressing, future expansion |
| Console | U16–U17 | Telescopic shelf — screen/keyboard/mouse |
| Airflow gap | U15 | Thermal separation — do not fill |
| Compute | U12–U14 | sccm-01, esxi-01, prx-01 |
| DC / expansion | U01–U11 | dc-01 tower on bottom shelf, U02–U11 free |

---

## Front Cabling Diagram

Network devices face front. Server ports face rear.

```
U34  ░░░░ Cable Manager
     │
U33  ████ 3850 (Gi ports face front)
          Gi1/0/1 ──[G]0.5m──→ 891F GE0            (routed WAN uplink)
          Gi1/0/2 ──[G]0.5m──→ 3560 GE9             (OOB switch uplink)
          Gi1/0/3 ──[W]0.5m──→ Patch Panel Port 1   (server data)
          Gi1/0/4 ──[W]0.5m──→ Patch Panel Port 2   (server data)
          Gi1/0/5 ──[W]0.5m──→ Patch Panel Port 3   (server data)
          Gi1/0/6 ──[W]0.5m──→ Patch Panel Port 4   (server data)
          Gi1/0/7 ──[W]0.5m──→ Patch Panel Port 5   (server data)
          Gi1/0/8 ──[W]0.5m──→ Patch Panel Port 6   (server data)
     │
U32  ████ PATCH PANEL (Digitus 24-port)
          ┌─ Ports  1- 6   ← [W]0.5m  from 3850     server data
          ├─ Ports  7-12   ← reserved                server data future
          ├─ Ports 13-17   ← [B]0.5m  from 3560      OOB management
          ├─ Ports 18-20   ← reserved                OOB future
          └─ Ports 21-24   ← reserved                uplinks / future
     │
U31  }
U30  } 891F (ports face front)
          GE0 ──[G]0.5m──→ 3850 Gi1/0/1             (routed WAN uplink)
          GE8 ──────────→  TP-Link unmanaged switch  (WAN/ISP split — outside rack scope)
     │
U29  }
U28  } 3560-CG (ports face front)
          GE1 ──[B]0.5m──→ Patch Panel Port 13       (iDRAC dc-01)
          GE2 ──[B]0.5m──→ Patch Panel Port 14       (iDRAC esxi-01)
          GE3 ──[B]0.5m──→ Patch Panel Port 15       (iDRAC prx-01)
          GE4 ──[B]0.5m──→ Patch Panel Port 16       (iLO sccm-01)
          GE5 ──[B]0.5m──→ Patch Panel Port 17       (D-Link OOB)
          GE9 ──[G]0.5m──→ 3850 Gi1/0/2              (OOB uplink)
```

---

## Rear Cabling Diagram

Server ports exit rear, dress up rear uprights to patch panel.

```
U34  ░░░░ Cable Manager       ← server upruns dressed here before patch panel rear ports
U33  ████ 3850                ← power: Schuko 2m → 19" power strip
U32  ████ Patch Panel         ← rear ports terminate all server runs
U31  }
U30  } 891F                   ← power: Schuko 2m → 19" power strip
     │                           WAN: cable to TP-Link unmanaged switch (outside rack)
U29  }
U28  } 3560-CG                ← power: Schuko 2m → 19" power strip
U27
│
│    ← cable corridor
│       [W] white 0.5m server bundles travel rear upright U12 → U34
│       power cables run left side to vertical HP PDUs ✅
│
U15                           ← airflow gap
U14  ████ prx-01              → [M][B][V] exit rear → upright → cable mgr U34 → patch panel rear
U13  ████ esxi-01             → [M][B][R][V] exit rear → upright → cable mgr U34 → patch panel rear
U12  ████ sccm-01             → [M][B] exit rear → upright → cable mgr U34 → patch panel rear
│
│    Power: Schuko cables left side → vertical HP PDUs ✅
│
U01  ──── dc-01 (T330)        → [M][B] longest run — MEASURE before ordering cable lengths
```

---

## Cable Inventory & Status

| Colour | Length | Purpose | VLAN | In hand | Status |
|--------|--------|---------|------|---------|--------|
| White | 0.5m | 3850 → Patch Panel / server upruns | — | 20× | ✅ |
| Green | 0.5m | Uplinks / trunks | — | 5× | ✅ |
| Blue | 0.5m | OOB management (3560 → Patch Panel) | VLAN 10 | 10× | 📦 incoming |
| Magenta | 0.25m | Server data | VLAN 30 | 5× | ✅ |
| Red | 0.25m | vMotion | VLAN 30 | 5× | ✅ |
| Violet | 0.25m | Storage | VLAN 40 | 5× | ✅ |
| Panduit Cat6 | 1/1.5/2/3m | Flexible / temporary use | — | mixed | ✅ |
| Schuko power | 2m | Network devices → 19" power strip | — | 5× | 📦 incoming |

---

## Key IP Reference

| Device | Hostname | Mgmt IP (VLAN 10) | Primary IP |
|--------|----------|-------------------|------------|
| Dell T330 | itc-uvy-dc-01 | 10.0.10.6 (iDRAC) | 10.0.20.2 |
| Dell R620 | itc-uvy-esxi-01 | 10.0.10.4 (iDRAC) | — |
| Dell R620 | itc-uvy-prx-01 | 10.0.10.3 (iDRAC) | — |
| HP DL360 Gen9 | itc-uvy-sccm-01 | 10.0.10.5 (iLO) | — |
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
- ⏳ Patch cable for dc-01 — measure rear upright run U01→U34 before ordering
- ✅ Vertical HP PDUs — installed, zero-U left side of rack
- ✅ Coloured patch cables (magenta, red, violet 0.25m / white, green 0.5m) — in hand
- ✅ 19" shelves installed (2U each)
- 🔔 dc-01 virtualisation (Phase 2) — will free U01–U11 entirely
- 🔔 Optical lines + 10GbE east-west (Phase 3) — C3850-NM-2-10G + R620 mezz NICs

---

## Design Decisions

- **Patch panel at U32** — centred in networking zone, 3850 directly above, router/OOB switch below. Minimises cable runs in both directions, logical hierarchy matches traffic priority
- **3850 at U33** — busiest device, directly adjacent to patch panel, shortest possible runs
- **891F at U30-31** — single routed uplink only, one green 0.5m to 3850
- **3560-CG at U28-29** — OOB only, less critical, handled by blue 0.5m to patch panel
- **Left = PDU side** — convention always left/right as viewed from front of rack
- **U15 airflow gap** — intentional, do not fill
- **Rear cable highway U18–U26** — intentional empty space for rear upright dressing
- **Port face direction** — network devices face front, servers face rear, patch panel is the cross-connect

---

## Notes

- All server airflow front-to-back — cable corridor U18–U26 keeps rear dressing clear of compute exhaust
- 19" shelves occupy 2U each — confirmed from physical installation
- dc-01 T330 has longest cable runs in rack (U01→U34) — measure before ordering
- Rack orientation convention: left/right always referenced from front of rack
- Blue 0.5m cables used for OOB runs (not 0.25m) — 3560 at U28 to patch panel at U32 exceeds 0.25m reach
