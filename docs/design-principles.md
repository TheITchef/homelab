# 📋 Design Principles

> Standing architectural decisions for the theITchef HomeLab.
> Established before build — followed throughout all phases.

---

## Principle 1 — GDPR Compliance by Default
Prefer EU GDPR compliant solutions for all components.
Where US-based hyperscalers are used, ensure data residency is explicitly set to EU regions.
Document every exception and its justification.

## Principle 2 — Azure Region
- Primary: **Sweden Central** (Stockholm)
- DR/Paired: **Sweden South**
- No exceptions without documented justification

## Principle 3 — Data Sovereignty
- Terraform state → EU region or self-hosted MinIO
- Personal data → never leaves EU boundary
- PII → on-premises only where possible

## Principle 4 — Security First
- Zero-trust architecture from day one
- MFA on all admin accounts (YubiKey 5C NFC)
- Break-glass procedures documented and tested
- Privileged Access Workstation (PAW) → T470s Ubuntu

## Principle 5 — Infrastructure as Code
- Everything documented and repeatable
- No manual changes without corresponding code/docs
- GitOps — GitHub as single source of truth

## Principle 6 — Observability Built In
- Monitoring and logging from day one
- SLO/SLI defined per service
- Alerting before problems become incidents

## Principle 7 — Open Source First
- Prefer open source solutions
- Avoid vendor lock-in where possible
- Commercial solutions must justify cost vs open source equivalent

---

*Last updated: 2026-03-08*
