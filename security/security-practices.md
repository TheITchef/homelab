# 🔒 Security Practices

> Security is not an afterthought — built in from day one.

---

## Privileged Access Workstation (PAW)

**Device:** Lenovo ThinkPad T470s
**OS:** Ubuntu 24.04 LTS + LUKS full disk encryption
**Purpose:** All infrastructure management from this machine only

PAW tools:
- KeePass2 — credential management
- Remmina — RDP to Windows servers
- SSH — Linux servers + network devices
- YubiKey 5C NFC — hardware MFA (pending delivery)
- Browser — iDRAC/iLO/vCenter/Azure

---

## Credential Management

**Tool:** KeePass2 (open source, local, GDPR compliant)
**Database:** theitchef-lab.kdbx
**Backup:** Google Drive (encrypted at rest)

### Account Tiers

| Tier | Account | Purpose | Usage |
|------|---------|---------|-------|
| 0 | ioannis@theitchef.com | Domain Admin | Daily admin tasks |
| 1 | itchef.admin@theitchef.com | Break-glass domain | When Tier 0 fails |
| 2 | localbreak.glass (disabled) | Local break-glass | When AD fails |
| 3 | DSRM password | AD recovery | Nuclear option |

---

## Break-Glass Procedure

```
Tier 0 fails → use Tier 1 (itchef.admin)
Tier 1 fails → enable Tier 2 (localbreak.glass)
              → fix issue
              → disable Tier 2 immediately
AD fails     → boot DSRM → use Tier 3
              → repair AD → normal boot
```

Rules:
- Never use break-glass for daily tasks
- Change password after every use
- Every use must be documented
- Quarterly test all break-glass accounts

---

## MFA Strategy

| Phase | Implementation |
|-------|---------------|
| Now | KeePass strong passwords |
| Phase 1 | YubiKey 5C NFC — FIDO2 + Smart Card |
| Phase 3 | HashiCorp Vault dynamic credentials |
| Phase 4 | Azure PIM JIT elevation |

---

## Windows Server Hardening Checklist

- [x] Rename Administrator account (localbreak.glass)
- [x] Disable Administrator account
- [x] Enable Windows Firewall all profiles
- [x] RDP enabled
- [ ] RDP restricted to PAW subnet
- [ ] Audit policy enabled
- [ ] Password policy configured
- [ ] LAPS deployment (Phase 3)

---

*Last updated: 2026-03-08*
