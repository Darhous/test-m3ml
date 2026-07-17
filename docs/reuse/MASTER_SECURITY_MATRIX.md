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
| immudb | No major pattern surfaced this Wave | Company-led (Codenotary) | Not independently audited | Cryptographic tamper-evidence holds even against a malicious DBA — strongest security-architecture property found in the program so far for Risk #25's threat class |
| Eramba / CISO Assistant / GovReady-Q | No major pattern surfaced this Wave | Company/community-led | Not independently audited | Internal governance tools, lower exposure profile than customer-facing components |

**Scope note (final, honest disclosure):** This table's dedicated
per-candidate CVE/disclosure-process rows were maintained at Modules 1-3
depth. For Modules 4-28, each Feature's own `06-security-review.md`
carries the equivalent finding (typically "no major CVE pattern
surfaced this pass, not independently audited" plus any notable signal
— e.g. OpenELIS Global's/openIMIS's/OpenBoxes's national-scale
production-hardening evidence, Mirth Connect's frozen-release risk,
Kill Bill's 10+-year regulated-industry track record). Not consolidated
into this table's row format to avoid fabricating a false impression of
independent security audit work that was not performed at that depth —
the per-Feature files are the authoritative record.
