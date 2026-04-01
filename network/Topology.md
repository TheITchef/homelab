# Lab Network Architecture — Current State & Planned Migration

## Overview

This document describes the **current network topology** and the **intended future design** for the lab environment.  
At present, the **Cisco Catalyst 3560CG** still performs **east‑west (inter‑VLAN) routing**, but this is a **temporary transitional state**.  
The long‑term plan is to migrate all Layer 3 functions to the **Cisco Catalyst 3850**, which will become the dedicated core switch.

---

## Current L3 Routing Architecture (Transitional State)

- The **Cisco Catalyst 3560CG** currently holds the SVIs and default gateways.
- All **east‑west traffic** (inter‑VLAN routing) flows through the 3560CG.
- The **Cisco Catalyst 3850** operates as a hybrid access/L2 aggregation switch.
- The **Cisco 891F** provides WAN/edge connectivity and NAT.

> **Note:** This is a temporary configuration.  
> The 3850 will assume full L3 responsibilities at the earliest convenient maintenance window.

---

## Target Architecture (Planned)

The intended design is:

- **Cisco Catalyst 3850** becomes the **core L3 switch**.
- All **SVIs, gateways, and inter‑VLAN routing** move to the 3850.
- The **3560CG** becomes a pure **access switch**.
- The **891F** remains the WAN/edge router.
- Native VLAN remains **999** across all trunks.

---

## VLANs & Subnets

| VLAN | Name     | Subnet          | Gateway (Current) | Gateway (Future) | Notes |
|------|----------|------------------|--------------------|-------------------|-------|
| 10   | MGMT     | 10.0.10.0/24     | 3560CG             | 3850              | Management network |
| 20   | LAN      | 10.0.20.0/24     | 3560CG             | 3850              | DC + PAW (in‑band mgmt) |
| 30   | SERVERS  | 10.0.30.0/24     | 3560CG             | 3850              | Server VLAN |
| 40   | STORAGE  | 10.0.40.0/24     | 3560CG             | 3850              | Storage/iSCSI |
| 50   | DMZ      | 10.0.50.0/24     | 3560CG             | 3850              | DMZ segment |
| 99   | WIFI     | 10.0.99.0/24     | 3560CG             | 3850              | Wireless |
| 999  | NATIVE   | —                | —                  | —                 | Native VLAN for trunks |

---

## Key Device Roles

| Device | Role | Notes |
|--------|------|-------|
| **Cisco 3850** | Future core L3 switch | Will own all SVIs and routing |
| **Cisco 3560CG** | Current L3 switch | Temporary; will become access‑only |
| **Cisco 891F** | WAN/edge router | NAT + upstream connectivity |
| **Dell T330 (DC)** | Domain Controller | VLAN 20; iDRAC Basic → no OOB |
| **PAW** | Admin workstation | VLAN 20 for in‑band DC access |

---

## Trunk Configuration (Current)

### 3850 → 891F (Gi1/0/1)

switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 1,2,10,20,30,40,50,99,999,1002-1005
Code


### 3850 → 3560CG (Gi1/0/2)

switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 1,2,10,20,30,40,50,99,999,1002-1005
Code


---

## Access Ports (Examples)

### Domain Controller (Dell T330) — Gi1/0/6

switchport mode access
switchport access vlan 20
spanning-tree portfast
Code


### PAW — Gi1/0/20 (example)

switchport mode access
switchport access vlan 20
spanning-tree portfast
Code


---

## Design Notes

- The **3560CG currently performs east‑west routing**, but this is temporary.
- The **3850 will become the core L3 switch** and take over all SVIs.
- VLAN 20 hosts both the **DC** and **PAW** because the T330 has **iDRAC Basic**, requiring in‑band management.
- All trunks use **native VLAN 999**.
- All VLANs are trunked end‑to‑end between **891F ↔ 3850 ↔ 3560CG**.

---

## Migration Plan (High‑Level)

1. Create SVIs on the 3850 (shutdown initially).
2. Copy IPs from 3560CG SVIs to 3850 SVIs.
3. Shut down SVIs on 3560CG.
4. No‑shutdown SVIs on 3850.
5. Verify routing, ARP, and inter‑VLAN reachability.
6. Remove L3 config from 3560CG.

---
