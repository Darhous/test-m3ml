# Feature: Authentication

**Module:** Identity and Access (Platform Kernel)
**Source (Discovery):** Wave 3 Capability "Security" (Category 9,
Governance); Constitution Section 21 (Backend-Enforced Authorization);
Bounded Context 27 (Identity and Access, Wave 9 Modeled tier — Evidenced).

## What This Feature Covers

Verifying the identity of every actor who reaches the platform: staff
(lab technicians, verifiers, finance, HR), practitioners, patients (portal
access), tenant admins, platform operators, and partner/API clients (9
Confirmed customer types, Discovery Section 7). Covers credential
verification, password policy, account lockout, and the login/logout
lifecycle — the layer everything else in this Module (SSO, MFA, Session
Management) sits on top of.

## Why It Matters

Universal dependency (Wave 10: Platform Kernel, "None — universal
dependency" in the Extraction Trigger column). Every one of the 28
Bounded Contexts and every one of the 39 personas (Wave 2) needs this
Feature working correctly before any other Module can be used. It is also
the anchor point for this program's Cross-Feature Dependency Map — a
single mature IAM engine solves this Feature plus 4 others in this Module
(see `MASTER_DEPENDENCY_MATRIX.md`).

## Constraints From Discovery

- Constitution Section 21: authorization must be Backend-enforced, not
  UI-only.
- Constitution Section 18/19: Multi-Tenant Isolation — authentication
  must be tenant-aware from day one (Risk Register #17/SEC-04, Highest
  severity, still Open on the exact partitioning mechanism).
- Constitution Section 23: every authentication event is Audit-relevant.
- No real medical/personal data may appear in this research (Constitution
  `CLAUDE.md` Section 13) — all examples below use fictitious data only.
