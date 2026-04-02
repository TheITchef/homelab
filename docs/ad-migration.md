# Active Directory Migration Runbook — itc‑uvy  
**From:** itc‑uvy‑dc‑01 (Dell T330, WS2016 Essentials)  
**To:** DC01‑VM (Windows Server 2025, Hyper‑V on DL360 Gen9)  
**Last updated:** 2026‑04‑02

---

# 🎯 Objective

Migrate Active Directory, DNS, and identity services from the legacy **Dell T330** to a new **virtualized domain controller** running on the DL360 Hyper‑V host.

This runbook ensures:

- Clean AD DS migration  
- Zero downtime for authentication  
- Safe FSMO transfer  
- DNS migration  
- Entra Connect readiness  
- Clean demotion of the T330  

---

# 🧱 Prerequisites

### Hyper‑V Host (DL360 Gen9)
- Windows Server 2025 Datacenter installed  
- Hyper‑V role enabled  
- VLAN 30 connectivity verified  
- iLO reachable on VLAN 10  

### Virtual Network
- VLAN 30 (SERVERS) reachable  
- DNS queries to T330 working  
- 3850 L3 core routing active  

### Legacy DC (T330)
- Healthy AD DS  
- SYSVOL replication healthy  
- Time sync correct  
- No lingering replication errors  

### Tools
- RSAT installed on PAW or MGMT01‑VM  
- Admin credentials for domain  

---

# 🖥️ Step 1 — Deploy the New DC VM (DC01‑VM)

### VM Specs
- OS: Windows Server 2025  
- vCPU: 2  
- RAM: 8–12GB  
- Disk: 60GB  
- NIC: VLAN 30  
- Name: **DC01‑VM**  
- IP: **10.0.30.x** (static)  
- DNS: **10.0.20.2** (legacy T330)  

### Steps
1. Create VM on Hyper‑V host  
2. Install Windows Server 2025  
3. Set static IP  
4. Join domain: `ad.theitchef.com`  
5. Reboot  

---

# 🏛️ Step 2 — Promote DC01‑VM to Domain Controller

On DC01‑VM:

1. Install AD DS role  
2. Promote to domain controller  
3. Add DNS role  
4. Reboot  
5. Verify replication:  

repadmin /replsummary
repadmin /showrepl
Code

6. Verify SYSVOL:  

net share
Code


---

# 🧬 Step 3 — Transfer FSMO Roles

On DC01‑VM:

netdom query fsmo
Code


Transfer roles:

Move-ADDirectoryServerOperationMasterRole -Identity DC01-VM -OperationMasterRole 0,1,2,3,4
Code


Verify:

netdom query fsmo
Code


---

# 🌐 Step 4 — Migrate DNS

On DC01‑VM:

1. Open DNS Manager  
2. Ensure forward lookup zones replicated  
3. Ensure reverse lookup zones replicated  
4. Update DHCP scopes (if any) to point to new DNS  
5. Update static DNS on servers:  
   - Primary: **DC01‑VM**  
   - Secondary: **T330** (temporary)

---

# 🔁 Step 5 — Replication & Health Validation

Run on both DCs:

dcdiag /v
repadmin /replsummary
repadmin /showrepl
Code


Check event logs:

- Directory Service  
- DNS Server  
- File Replication Service / DFS‑R  

---

# 🔐 Step 6 — Update Time Services

On DC01‑VM (new PDC Emulator):

w32tm /config /manualpeerlist:"pool.ntp.org" /syncfromflags:manual /reliable:yes /update
w32tm /resync
Code


On T330:

w32tm /config /syncfromflags:domhier /update
Code


---

# ☁️ Step 7 — Prepare for Entra Connect

On DC01‑VM:

- Ensure DNS resolves internal + external  
- Ensure outbound HTTPS allowed  
- Ensure domain functional level is correct  
- Ensure UPN suffix is correct (`theitchef.com`)  

---

# 🧹 Step 8 — Demote the T330 (Legacy DC)

On T330:

1. Ensure DC01‑VM holds all FSMO roles  
2. Ensure DNS is working from DC01‑VM  
3. Ensure SYSVOL is healthy  
4. Run:  

dcpromo
Code

5. Remove AD DS role  
6. Reboot  
7. Remove from domain  
8. Shut down or repurpose  

---

# 🧼 Step 9 — Clean Up AD Metadata

On DC01‑VM:

ntdsutil
metadata cleanup
Code


Remove old DC entries:

- Sites and Services  
- DNS A records  
- DNS NS records  
- DHCP scopes (if any)  

---

# 🧪 Step 10 — Validation

### Authentication
- Log in with domain account  
- Test GPO application  
- Test DNS resolution  

### Replication

repadmin /replsummary
Code


### Event Logs
- Directory Service  
- DNS Server  
- System  

---

# 🚀 Step 11 — Deploy AADC01‑VM (Entra Connect)

After AD is stable:

1. Deploy AADC01‑VM  
2. Install Entra Connect  
3. Configure sync  
4. Validate cloud identities  

---

# 📦 Step 12 — Backup & Snapshot Strategy

### Recommended:
- Veeam CE for VM‑level backups  
- Pre‑change snapshots for:  
  - Schema updates  
  - Entra Connect upgrades  
  - GPO changes  

---

# 📝 Notes

- T330 is now **legacy** and can be repurposed (NAS, TrueNAS, lab node)  
- All Microsoft services now run on Hyper‑V  
- AD is fully virtualized and portable  
- Network core (3850) handles all routing  

---

*Tags: #activedirectory #migration #entra #dns #homelab #hyperv #windowsserver*