# Rack Layout — itc‑uvy — HP 10642G2 42U  
**Site:** Upplands Väsby (uvy)  
**Rack:** HP 10642G2 42U | U1 = bottom  
**Last updated:** 2026‑04‑02

---

## Current Layout (Revised 2026)

U42
U41
U40
U39
U38 ──── Shelf    }
U37 ────          }  TP‑Link Archer AX11 + D‑Link DGS‑1100‑08V2  (OOB mgmt / home AP)
U36 ──── Shelf    }
U35 ────          }  itc‑uvy‑rtr‑01  Cisco 891F   Edge/WAN/NAT   ← ports REAR
U34                  (free — buffer U between 891F shelf and 3850)
U33 ████ itc‑uvy‑sw‑02  Cisco 3850‑48P‑E   Core L3 (active)   ← ports FRONT
U32 ████ Patch Panel    Digitus 24‑port     ← cable routing bar behind
U31 ──── Shelf    }
U30 ────          }  itc‑uvy‑sw‑01  Cisco 3560‑CG  OOB switch only  ← ports FRONT
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
U14 ████ itc‑uvy‑esxi‑02  Dell R620 (1CCL5Y1)         ESXi 8        ✓ RACKED
U13 ████ itc‑uvy‑prx‑01   Dell R620 (H2718X1)         Proxmox       ✓ RACKED
U12 ████ itc‑uvy‑ms‑01    HP DL360 Gen9 (CZJ54302TB)  Hyper‑V host  
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
U01 ──── Shelf         itc‑uvy‑dc‑01 (Dell T330)      Legacy — to be demoted
Code

