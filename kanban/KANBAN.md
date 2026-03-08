# 📋 HomeLab Kanban

---

## Done

- [x] Hardware inventory — all 4 servers documented
- [x] Ubuntu 24.04 LTS + LUKS encryption on T470s
- [x] KeePass2 setup + all credentials populated
- [x] Windows Server 2016 Essentials updates complete
- [x] DC01 promoted → ad.theitchef.com
- [x] OU structure created (_THEITCHEF)
- [x] Admin accounts created (ioannis, itchef.admin)
- [x] Service accounts created (6 accounts)
- [x] MotoGP grid users created (People OU)
- [x] localbreak.glass renamed + disabled
- [x] RDP enabled on DC01
- [x] Remmina installed on T470s
- [x] GitHub repo initialised
- [x] YubiKey ordered (5C NFC + 5 NFC)

---

## In Progress

- [ ] AD security hardening (password policy, audit policy)
- [ ] GitHub repo first push
- [ ] LinkedIn post #1 draft

---

## Backlog — Phase 1

- [ ] Cisco 891F initial configuration
- [ ] Cisco 3560-CG VLAN configuration
- [ ] D-Link OOB switch configuration
- [ ] Physical rack build + cabling
- [ ] Assign static OOB IPs (VLAN 10)
- [ ] iDRAC/iLO default passwords changed
- [ ] YubiKey setup (when delivered)

---

## Backlog — Phase 2

- [ ] ESXi 8.0.0 → 8.0 Update 3
- [ ] vCenter Server deployment
- [ ] vSphere cluster configuration
- [ ] vDS networking
- [ ] NFS datastore
- [ ] VM templates

---

## Backlog — Phase 3

- [ ] Certificate Authority
- [ ] SCCM/MECM + SQL Server
- [ ] Prometheus + Grafana
- [ ] Loki logging
- [ ] Backup solution
- [ ] HashiCorp Vault
- [ ] LAPS deployment

---

## Backlog — Phase 4

- [ ] Azure AD Connect
- [ ] Site-to-site VPN
- [ ] Azure Arc
- [ ] Azure Policy
- [ ] Azure Defender for Servers

---

## Backlog — Phase 5

- [ ] Docker + k3s cluster
- [ ] Helm + ArgoCD GitOps
- [ ] AKS + Arc-enabled K8s
- [ ] PostgreSQL + Redis
- [ ] Terraform + Ansible
- [ ] Ollama local LLMs
- [ ] MLflow

---

## Known Issues

| Host | Issue | Priority |
|------|-------|----------|
| esxi-01 | Non-Dell drive alert | Low |
| esxi-01 | PSU2 not cabled | Low |
| esxi-02 | PSU1 fault history | Monitor |
| esxi-02 | H710 BBU unknown | Check |
| mgmt-01 | iLO timeout short | Low |
| mgmt-01 | P440ar cache/BBU unknown | Check |
| All | Default OOB passwords | High |

---

*Last updated: 2026-03-08*
