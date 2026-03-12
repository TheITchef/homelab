---
tags: [shortcuts, git, ssh, cisco, ubuntu, network, reference, keepass, nano]
---

# Scripts & Shortcuts — theITchef HomeLab
**Last updated:** 2026-03-11  
**Author:** Ioannis (theITchef)  
> A living reference. Add to this every time you find a useful command or shortcut.

---

## Git Workflow

### Daily work — commit everything at once
```bash
cd ~/homelab
git add .
git commit -m "your message"
git push
```

### Branch check before committing
```bash
git branch                    # check current branch
git checkout dev              # switch to dev if on master
```

### End of milestone — merge dev to master
```bash
git checkout master
git merge dev
git push
git checkout dev              # always go back to dev
```

### Untrack a file already in git
```bash
git rm --cached <filename>
echo "<filename>" >> .gitignore
git add .gitignore
git commit -m "Untrack <filename>"
```

---

## SSH

### SSH to 3560-CG (legacy IOS — requires flags)
```bash
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -oCiphers=+aes256-cbc admin@10.0.10.11
```

### SSH to 3560-CG using config shortcut (after setup)
```bash
ssh 3560cg
```

### T470s SSH config (~/.ssh/config)
```
Host 3560cg
    HostName 10.0.10.11
    User admin
    KexAlgorithms +diffie-hellman-group1-sha1
    HostKeyAlgorithms +ssh-rsa
    Ciphers +aes256-cbc

Host 3850
    HostName 10.0.10.12
    User admin

Host 891f
    HostName 10.0.10.1
    User admin
```

---

## Network — T470s

### Check current IP
```bash
ip addr show enp0s31f6
```

### Add temporary static IP (for direct iDRAC access)
```bash
sudo ip addr add 192.168.0.100/24 dev enp0s31f6
sudo ip addr add 10.0.10.100/24 dev enp0s31f6
```

### Remove temporary static IP
```bash
sudo ip addr del 192.168.0.100/24 dev enp0s31f6
sudo ip addr del 10.0.10.100/24 dev enp0s31f6
```

### Flush and renew DHCP
```bash
sudo ip addr flush dev enp0s31f6
sudo dhclient enp0s31f6
```

### Check DNS resolution
```bash
resolvectl status | grep DNS
```

---

## Ubuntu Maintenance

### Update system
```bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove -y
```

### Check open ports
```bash
ss -tulnp
```

---

## Cisco IOS — Useful Commands

### Save config
```
wr
```

### Verify trunk
```
show interfaces trunk
```

### Verify VLANs
```
show vlan brief
```

### Verify routing
```
show ip route
show ip interface brief
```

### Verify SSH sessions
```
show users
```

### Safe debug (always filter!)
```
access-list 199 permit ip host <your-ip> any
debug ip packet 199
undebug all
```

---

## Nano

### Save and exit
```
Ctrl+X → Y → Enter
```

### Exit without saving
```
Ctrl+X → N
```

---

## KeePass

### Password generation recommendation
- Length: 32 characters
- Include: uppercase, lowercase, numbers, symbols
- One unique password per device — never reuse

---

*Add new entries as you discover them.*  
*github.com/TheITchef/homelab · docs/scripts-and-shortcuts.md*
