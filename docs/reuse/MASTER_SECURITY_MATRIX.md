# Master Security Matrix

Every candidate's security posture as found in its own repository (CVE
history, disclosure process, dependency hygiene, security-relevant
architecture). Detail lives in each Feature's `06-security-review.md`.
This matrix records findings only — it does not itself constitute a
security sign-off for adoption (Constitution Section 37, security
testing/accepted-risk-with-owner discipline still applies at
implementation time).

| Repository | Known CVE History | Disclosure Process | Dependency Hygiene | Notable Concern |
|---|---|---|---|---|
| Keycloak | Active, real (~88 CVEs across lifetime; 10+ fixed across 3 point releases Feb–Apr 2026 alone: CVE-2025-14083, CVE-2026-1002/3429/4634/4636/3872, CVE-2026-1035, CVE-2025-14777/14082, CVE-2026-3121) | Public — CVE.org / Red Hat Security Advisories / GitHub Security Advisories, active | Not independently audited in this pass; frequent point releases suggest active dependency tracking | Requires an explicit, budgeted patch-cadence commitment — treated as Medium residual risk, not disqualifying |
| Open Policy Agent | No major pattern surfaced this Wave | CNCF Graduated — includes a formal security-audit history as part of graduation | Not independently audited in this pass | Lower external scrutiny than Keycloak historically, treated as neutral (not a point in its favor) |
| Zitadel | Less history surfaced (newer, smaller install base) | Company-led | Not independently audited | Lower visibility ≠ better security — treated as neutral evidence |
| Authentik | Same caveat as Zitadel | Company-led | Not independently audited | Same caveat |
