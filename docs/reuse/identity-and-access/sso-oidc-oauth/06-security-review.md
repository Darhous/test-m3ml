# Security Review — SSO / OIDC / OAuth

Inherits `../authentication/06-security-review.md` in full. One
feature-specific item found in the same search: **CVE-2026-3872
(redirect URI validation bypass, fixed in Keycloak 26.5.7)** is directly
an OAuth2/OIDC-flow vulnerability class (open redirect in the
authorization-code flow), not a generic authentication bug — logged here
specifically because it is this Feature's most directly relevant CVE.
Confirms the same conclusion: Medium residual risk, mitigated by active
patch-cadence commitment, not a rejection reason.
