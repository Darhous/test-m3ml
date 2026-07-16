# Global Search Log — Authentication

## Search Scope

GitHub, GitLab, CNCF Landscape, Eclipse Foundation, Apache Foundation,
official vendor/foundation documentation, independent comparison
publications (2026-dated where available, since currency matters for a
security-relevant component).

## Queries Run (via WebSearch, live, 2026-07-16)

1. `open source identity access management 2026 Keycloak vs Ory vs
   Authentik vs Zitadel enterprise comparison`
2. `Keycloak multi-tenancy healthcare production adoption 2026`
3. `Keycloak CVE security history vulnerabilities 2025 2026`

## Landscape Notes

The open-source IAM space has 4 credible mature players as of 2026:
**Keycloak** (Red Hat/IBM-backed, CNCF-incubated, largest community),
**Zitadel** (Go, event-sourced, cloud-native, switched Apache 2.0 → AGPL
3.0 in 2025), **Authentik** (Python/Go, MIT core + commercial enterprise
tier, strongest in self-hosting/SME segment), **Ory** (microservices
decomposition — Kratos for identity, Hydra for OAuth2/OIDC, separately
composable rather than one monolith). FusionAuth appeared in search
results as a commercial-core alternative (source-available, not fully
OSS) — noted but not carried forward as a primary candidate since it does
not meet this program's "existing Service/Engine" open-source-first
framing as cleanly as the 4 above.

## Candidates Carried Forward

Keycloak, Zitadel, Authentik, Ory (Kratos + Hydra as a pair). 4 candidates
— fewer than 10 because the space genuinely narrows to 4 mature,
non-abandoned, enterprise-adopted options; no artificial padding to reach
10, per the program's explicit instruction ("if only three excellent
candidates exist, report three").
