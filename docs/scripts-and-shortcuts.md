# Scripts & Shortcuts — theITchef HomeLab
**Last updated:** 2026-03-12

---

## SSH Shortcuts (T470s PAW — ~/.ssh/config)

```
Host 3560cg
    HostName 10.0.10.11
    User admin
    KexAlgorithms +diffie-hellman-group1-sha1
    HostKeyAlgorithms +ssh-rsa
    Ciphers +aes256-cbc

Host idrac-prx
    HostName 10.0.10.3
    User itchef-admin

Host idrac-esxi
    HostName 10.0.10.4
    User itchef-admin

Host ilo-sccm
    HostName 10.0.10.5
    User itchef-admin
```

Usage: `ssh 3560cg` / `ssh idrac-prx` etc.

---

## Cable Colour Reference

| Colour | Length | Use |
|--------|--------|-----|
| 🟣 Magenta | 0.25m | Server data NICs |
| 🔵 Blue | 0.25m | iDRAC / iLO OOB |
| 🔴 Red | 0.25m | vMotion |
| 🟣 Violet | 0.25m | Storage |
| ⬜ White | 0.5m | Patch panel → 3850 runs |
| 🟢 Green | 0.5m | Uplinks / trunk ports |

All 1aTTack.de Cat.6 from Amazon.se — ordered 2026-03-12.

---

## iDRAC XML Hardware Inventory Export

Pull full hardware inventory via iDRAC REST API (no iDRAC Enterprise web UI needed for this):

```bash
curl -sku itchef-admin:PASSWORD \
  https://10.0.10.4/redfish/v1/Managers/iDRAC.Embedded.1/Actions/Oem/DellManager.ExportSystemInventory \
  -H "Content-Type: application/json" \
  -d '{"ExportURI":"local"}' -o hardware.xml
```

Or from iDRAC web UI: **Overview → Server → Inventory → Export**.

---

## DIMM Population Check (Python — from XML export)

```python
import xml.etree.ElementTree as ET

tree = ET.parse('HardwareInventory.xml')
root = tree.getroot()

for comp in root.iter('Component'):
    if comp.get('Classname') == 'DCIM_MemoryView':
        props = {p.get('NAME'): (p.find('VALUE').text if p.find('VALUE') is not None else None)
                 for p in comp.iter('PROPERTY')}
        print(f"{props.get('FQDD'):25} {int(props.get('Size',0))//1024}GB  {props.get('Speed')}MHz  {props.get('PartNumber')}")
```

---

## Useful Cisco IOS Commands

```
# Show all interfaces status
show interfaces status

# Verify VLAN trunk
show interfaces trunk

# Verify spanning tree
show spanning-tree summary

# Show CDP neighbours
show cdp neighbors detail

# Save config
write memory
```

---

## netplan DNS config (T470s PAW)

`/etc/netplan/01-netcfg.yaml`:
```yaml
network:
  version: 2
  ethernets:
    enp0s31f6:
      dhcp4: true
      nameservers:
        addresses: [10.0.20.2, 8.8.8.8]
```
Apply: `sudo netplan apply`

Verify: `resolvectl status` — should show 10.0.20.2 as primary DNS.
