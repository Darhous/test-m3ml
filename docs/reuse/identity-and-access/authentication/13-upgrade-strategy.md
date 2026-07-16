# Upgrade Strategy — Authentication

## Observed Release Cadence

Keycloak ships point releases roughly monthly (26.5.4 → 26.5.6 → 26.5.7
across February–April 2026 per `06-security-review.md`), several of which
carried security fixes. This is a real, evidenced cadence — not an
assumption.

## Recommended Posture (Recommended, not yet Confirmed)

- Track Keycloak's own release notes and CVE advisories as a standing
  operational input (not a one-time adoption decision).
- Keep the Anti-Corruption Layer (`09-integration-options.md`) as the
  sole integration surface, so a Keycloak version upgrade — or, in the
  worst case, a future migration away from Keycloak — touches one owned
  Module, not every consuming Module. This is the primary architectural
  payoff of the Adapter pattern for upgrade risk specifically.
- Pin to Keycloak's documented supported-version window rather than
  always-latest, balancing security-patch currency against upgrade churn
  — the exact policy (N-1 vs. always-latest) is an SAD-level operational
  decision, not decided here.

## Exit Path (if ever needed)

Because the Adapter speaks standard OIDC/OAuth2 (not a Keycloak-
proprietary protocol) to the rest of the platform, a future migration to
Zitadel, Authentik, or another OIDC-compliant IdP would require
re-pointing the Adapter's configuration and re-implementing any
Keycloak-specific Admin-API calls (tenant/Organization provisioning) —
a bounded, estimable migration, not a platform-wide rewrite. This
bounded-exit property is itself a reason the Engine + Adapter pattern was
chosen over direct embedding.
