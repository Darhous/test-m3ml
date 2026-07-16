# Architecture Review — Authentication

| Dimension | Keycloak | Zitadel | Authentik | Ory |
|---|---|---|---|---|
| Deployment model | Single Java service (Quarkus-based since v17+), clusterable | Single Go binary, event-sourced (CQRS/Event Sourcing internally) | Python (Django-based) + Go outposts, multi-process | Multiple independent Go services (Kratos, Hydra) — true microservices |
| Multi-tenancy primitive | Realm-per-tenant (classic) **or** Organizations-within-a-realm (stabilized Keycloak 26, 2024) | Native multi-tenant "Organization" concept, built in from the event-sourced core | Multi-tenant via "Brands"/Tenants, less mature than Keycloak's Organizations | No built-in tenant concept — tenancy must be modeled by the adopting application on top |
| Protocol standards | OIDC, OAuth2, SAML 2.0, LDAP federation | OIDC, OAuth2 (SAML via extension) | OIDC, OAuth2, SAML 2.0, LDAP, SCIM | OIDC/OAuth2 (Hydra is OpenID Foundation certified) |
| Extensibility | Java SPI (Service Provider Interface) — deep, battle-tested extension points (event listeners, custom authenticators, custom user storage) | Go-based, plugin surface newer/thinner than Keycloak's SPI | Python "Blueprints" + Go outposts for edge proxying | Each service has its own extension surface; more integration work to compose |
| Admin console | Full-featured, mature | Modern, clean, fewer advanced screens than Keycloak | Most polished UI among the 4 (frequently cited) | No unified admin console — Ory Console is a separate managed-cloud product |

## Fit Against This Platform's Architectural Constraints

- **Constitution Section 21 (Backend-Enforced):** all 4 candidates enforce
  token validation server-side; none rely on client-side trust.
- **ADR 0005 (Hybrid Tenant Isolation):** Keycloak's Organizations feature
  (stabilized 2024, Keycloak 26) is the closest existing-engine match to
  the platform's own still-Open shared-tier question (`open-questions.md`
  #15) — it does not answer that question, but it is compatible with
  either resolution (a tenant-ID-style Organization inside a shared
  realm, or a dedicated realm for a Dedicated-tier tenant), which is a
  genuine architectural strength for this specific platform.
- **Constitution Section 8 (One Owning Module Per Bounded Context):**
  Ory's microservices decomposition would require the platform to own
  more integration glue (composing Kratos + Hydra + a chosen admin UI)
  than Keycloak or Authentik, which ship as a more complete unit —
  working against the Modular Monolith direction (`CLAUDE.md` Section 7)
  by adding more moving parts than this Feature's scope requires.
