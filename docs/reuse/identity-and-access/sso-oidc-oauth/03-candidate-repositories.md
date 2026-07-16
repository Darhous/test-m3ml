# Candidate Repositories — SSO / OIDC / OAuth

Same 4 candidates as `../authentication/03-candidate-repositories.md`
(Keycloak, Zitadel, Authentik, Ory). Feature-specific differentiator:
**Identity Brokering / federation maturity**.

| Candidate | Federation (external IdP) | Acts as OIDC/OAuth2 Provider | SAML Support |
|---|---|---|---|
| Keycloak | Mature (Identity Brokering, long-standing) | Yes | Yes |
| Zitadel | Supported, newer | Yes | Via extension |
| Authentik | Supported (SCIM + federation) | Yes | Yes |
| Ory (Hydra) | N/A (Hydra is OAuth2/OIDC-only; federation would need Kratos + custom glue) | Yes — OpenID Foundation certified | No |
