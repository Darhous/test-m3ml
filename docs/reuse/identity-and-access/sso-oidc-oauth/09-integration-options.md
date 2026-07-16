# Integration Options — SSO / OIDC / OAuth

Same Anti-Corruption Layer pattern as `../authentication/
09-integration-options.md`. Feature-specific addition: for the
partner/API client customer type (9th Confirmed customer type), the
platform's Identity and Access Adapter additionally exposes a
Client-Credentials-grant OAuth2 flow (machine-to-machine, no user
present) — a standard Keycloak client type, not custom-built.
