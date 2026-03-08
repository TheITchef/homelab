# Architecture Decision Records

> Running log of decisions made during the homelab build.

---

## ADR-001 — T330 keeps Windows Server 2016 Essentials
- **Date:** 2026-03-06
- **Decision:** Do not wipe Dell T330. Keep OEM Windows Server 2016 Essentials licence.
- **Reason:** OEM licence is tied to hardware, cannot be transferred. Reinstall as NAS/file server role within WS2016.

## ADR-002 — 3560CG as ToR switch
- **Date:** 2026-03-06
- **Decision:** Use WS-C3560CG-8PC-S as Top of Rack switch.
- **Reason:** 8x PoE ports sufficient for Phase 1 (4 servers + router + OOB + WiFi + spare). SFP uplinks available for future expansion.
- **Constraint:** ipbase licence — inter-VLAN routing via router-on-a-stick on 891F.

## ADR-003 — 891F as edge router
- **Date:** 2026-03-06
- **Decision:** Use Cisco C891F-K9 as edge router.
- **Reason:** advipservices licence (full routing suite + VPN hardware module). Ideal for future site-to-site VPN to cloud in Phase 4.

## ADR-004 — D-Link as OOB management switch
- **Date:** 2026-03-06
- **Decision:** Use D-Link DGS-1100-08V2 exclusively for out-of-band management (iDRAC/iLO).
- **Reason:** 8 ports exactly matches number of OOB interfaces. Isolates management plane from production traffic.

## ADR-005 — Intermittent lab operation
- **Date:** 2026-03-06
- **Decision:** Lab operates intermittently for power saving until at least July.
- **Impact:** Heat/airflow not critical for Phase 1. D-Link OOB switch stays always-on for remote wake capability. TP-Link AX12 stays always-on.

## ADR-006 — iDRAC tiers
- **Date:** 2026-03-06
- **Decision:** R620 ×2 have iDRAC Enterprise. T330 has iDRAC Basic.
- **Impact:** T330 OS install and initial setup must be done physically on-site. R620s can be fully managed remotely.
