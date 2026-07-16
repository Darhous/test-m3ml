# Global Search Log — SSO / OIDC / OAuth

Reuses the `authentication` Feature's search pass (`../authentication/
02-global-search.md`) — the same 4 candidates were evaluated for identity
provisioning, so no separate search round was run. One additional,
narrower search was run specific to this Feature's federation angle:

## Additional Query

`Keycloak identity broker external IdP federation SAML OIDC enterprise
customer 2026`

Result: Keycloak's Identity Brokering feature (federating an external
IdP as a login option, mapping external claims to local users) is a
long-standing, mature Keycloak capability (predates the Organizations
feature) — directly reusable for the "hospital/corporate provider already
runs its own IdP" scenario without additional research beyond confirming
the feature exists and is stable, which it is.
