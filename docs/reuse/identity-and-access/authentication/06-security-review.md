# Security Review — Authentication

## Keycloak

Real, dated findings (WebSearch, 2026-07-16): actively disclosed and
patched — Keycloak 26.5.7 (April 2026) fixed CVE-2025-14083 (Admin REST
API improper access control / info disclosure), CVE-2026-1002 (Vert.x
static handler cache manipulation), CVE-2026-3429 (improper access
control for LoA during credential deletion), CVE-2026-4634 (DoS via scope
processing), CVE-2026-4636 (UMA policy resource injection), CVE-2026-3872
(redirect URI validation bypass). 26.5.6 (March 2026) fixed
CVE-2026-1035 (refresh token reuse via TOCTOU race), CVE-2025-14777
(IDOR in realm client management), CVE-2025-14082, CVE-2026-3121
(privilege escalation), plus information-disclosure issues. Historical
volume (~88 CVEs across the product's lifetime per aggregator sites) is
consistent with a widely-deployed, actively-scrutinized enterprise
product with a functioning disclosure process — not a red flag by itself,
but the **volume and recency both matter**: this platform must budget for
a real patch-management process (Constitution Section 34, Reliability;
Section 37, Security Testing) rather than treat "we adopted Keycloak" as
a one-time security decision.

## Zitadel

Less independent CVE history surfaced in this search than Keycloak (newer
project, smaller deployed base to date) — this is itself a finding: less
CVE history is not evidence of better security, it may simply reflect
less scrutiny and lower attacker/researcher attention. Treated as neutral
evidence, not a point in Zitadel's favor.

## Authentik

No major CVE pattern surfaced in this search round; same caveat as
Zitadel applies (smaller install base, less external scrutiny to date).

## Ory

Hydra's OpenID Foundation certification (Feature `sso-oidc-oauth`,
`03-candidate-repositories.md`) is itself a security-relevant signal —
conformance certification implies external protocol-correctness testing
beyond the project's own test suite.

## Disclosure Process

Keycloak: CVE.org / Red Hat Security advisories, public GitHub Security
Advisories, active. This is the most externally-verifiable disclosure
process of the 4 candidates, a direct byproduct of Red Hat/IBM stewardship
and CNCF incubation.

## Conclusion for This Feature

Keycloak's higher visible CVE count is evidence of scale and scrutiny, not
disqualifying — treated as a **Medium** residual risk requiring an
explicit patch-cadence commitment (see `12-risk-analysis.md`), not a
rejection reason.
