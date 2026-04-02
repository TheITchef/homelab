# Core SVI Migration — Cisco 3850 L3 Cutover  
**From:** Cisco 3560‑CG (legacy L3)  
**To:** Cisco 3850‑48P‑E (active L3 core)  
**Last updated:** 2026‑04‑02

---

# 🎯 Objective

Migrate all Layer‑3 interfaces (SVIs), routing, and gateway responsibilities from the **Cisco 3560‑CG** to the **Cisco 3850‑48P‑E**, which is now the primary core switch in the itc‑uvy rack.

This runbook ensures:

- Zero downtime for VLANs  
- Clean SVI migration  
- Correct trunking and uplinks  
- Updated default gateways  
- Verified routing and reachability  
- Safe decommissioning of L3 features on the 3560  

---

# 🧱 Prerequisites

### Hardware
- Cisco 3850 installed at U33  
- Cisco 3560‑CG at U30–31 (OOB‑only after migration)  
- Patch panel mapping validated (see rack-layout.md)

### Network
- VLANs defined: 10, 20, 30, 40, 50, 99, 999  
- 891F uplink connected to 3850 Gi1/0/1  
- 3560 uplink connected to 3850 Gi1/0/2  
- All server NICs patched to 3850 via PP

### Software
- IOS XE 16.6.7 on 3850  
- ipservicesk9 license active  
- SSH enabled  
- Config backed up

---

# 🧩 Step 1 — Prepare the 3850 for L3 Operation

Enable IP routing:

conf t
ip routing
end
wr mem
Code


Verify:

show ip route
Code


---

# 🌐 Step 2 — Create SVIs on the 3850

### VLAN 10 — MGMT

interface Vlan10
ip address 10.0.10.1 255.255.255.0
no shut
Code


### VLAN 20 — LAN

interface Vlan20
ip address 10.0.20.1 255.255.255.0
no shut
Code


### VLAN 30 — SERVERS

interface Vlan30
ip address 10.0.30.1 255.255.255.0
no shut
Code


### VLAN 40 — STORAGE

interface Vlan40
ip address 10.0.40.1 255.255.255.0
no shut
Code


### VLAN 50 — DMZ

interface Vlan50
ip address 10.0.50.1 255.255.255.0
no shut
Code


### VLAN 99 — WIFI

interface Vlan99
ip address 10.0.99.1 255.255.255.0
no shut
Code


### VLAN 999 — Native

interface Vlan999
description Native VLAN (hardened)
no ip address
no shut
Code


---

# 🔗 Step 3 — Configure Uplinks

### 891F → 3850 (Gi1/0/1)

interface Gi1/0/1
description Uplink to 891F
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,99,999
spanning-tree portfast trunk
Code


### 3560 → 3850 (Gi1/0/2)

interface Gi1/0/2
description Uplink to 3560 (OOB)
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,999
spanning-tree portfast trunk
Code


---

# 🖥️ Step 4 — Move Default Gateways to the 3850

On the 3560:

conf t
interface Vlan10
shutdown
interface Vlan20
shutdown
interface Vlan30
shutdown
interface Vlan40
shutdown
interface Vlan50
shutdown
interface Vlan99
shutdown
end
wr mem
Code


**Do NOT delete them yet** — just shut them down.

---

# 🔁 Step 5 — Routing Verification

On the 3850:

show ip route
show ip interface brief
show vlan brief
Code


Test from PAW (10.0.10.21):

ping 10.0.20.1
ping 10.0.30.1
ping 10.0.40.1
ping 10.0.50.1
Code


Test inter‑VLAN:

ping 10.0.20.10
ping 10.0.30.10
Code


---

# 🌍 Step 6 — Internet & NAT Verification

From a server VM:

ping 8.8.8.8
nslookup microsoft.com
Code


On the 891F:

show ip route
show ip nat translations
Code


---

# 🧼 Step 7 — Clean Up the 3560 (Convert to OOB‑Only)

On the 3560:

conf t
no ip routing
interface range Vlan10,20,30,40,50,99
no ip address
shutdown
end
wr mem
Code


Remove trunk VLANs:

interface Gi0/9
switchport trunk allowed vlan 10,999
Code


---

# 🧪 Step 8 — Final Validation

### Check:
- All VLANs reachable  
- All gateways reachable  
- DHCP relay (if used) working  
- DNS resolution working  
- Internet access working  
- No spanning‑tree flaps  
- No duplicate gateways  

### Commands:

show spanning-tree
show cdp neighbors
show ip arp
show mac address-table
Code


---

# 📦 Step 9 — Backup Final Configs

On 3850:

wr mem
copy running-config startup-config
Code


On 3560:

wr mem
Code


---

# 📝 Notes

- 3850 is now the **authoritative L3 core**  
- 3560 is **OOB‑only** and should not carry production VLANs  
- All servers and hypervisors use the 3850 as their default gateway  
- Patch panel mapping updated in rack-layout.md  
- This migration aligns with the 2026 architecture revision  

---

*Tags: #cisco #networking #l3core #svi #homelab #migration*