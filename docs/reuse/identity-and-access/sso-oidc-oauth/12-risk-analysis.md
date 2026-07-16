# Risk Analysis — SSO / OIDC / OAuth

Inherits `../authentication/12-risk-analysis.md` in full. One additional
feature-specific risk: **misconfigured Identity Brokering claim mapping**
could let an external IdP assert a role/Organization membership the
platform did not intend (a real, industry-known federation
misconfiguration class) — mitigated by the platform's Adapter layer
re-validating claims against its own Role/Organization model rather than
trusting brokered claims verbatim (Constitution Section 21, Backend-
Enforced). Likelihood: Low-Medium (requires misconfiguration, not a
product defect). Impact: High (authorization bypass). Owner: Identity and
Access Module.
