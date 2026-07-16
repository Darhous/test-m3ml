# Candidate Repositories — Authentication

| Candidate | Repository | Language | Governance | First Release | Latest Activity (as of search) |
|---|---|---|---|---|---|
| Keycloak | `keycloak/keycloak` | Java | CNCF Incubating; Red Hat/IBM primary steward | 2014 (originally Red Hat SSO) | Active — 26.5.7 released April 2026, monthly point-release cadence |
| Zitadel | `zitadel/zitadel` | Go | Company-led (ZITADEL GmbH), open-core | 2020 | Active — regular releases, event-sourced architecture |
| Authentik | `goauthentik/authentik` | Python + Go | Company-led (Authentik Security), open-core | 2018 | Active — frequent releases, large self-hosting community |
| Ory (Kratos + Hydra) | `ory/kratos`, `ory/hydra` | Go | Company-led (Ory Corp), CNCF-adjacent | Kratos 2019, Hydra 2015 | Active — Hydra is OpenID Foundation certified |

## Why These 4 and Not More

Every other result surfaced in search (FusionAuth, SuperTokens, Casdoor,
WSO2 Identity Server) was either source-available-not-fully-OSS
(FusionAuth), narrower in scope (SuperTokens — auth-only, no admin
console/federation depth), less enterprise-adopted with thinner
independent verification of production healthcare use (Casdoor), or a
much heavier full-suite product with a steeper adoption cost than this
Feature's scope justifies (WSO2). Not rejected as *bad* — simply not
among the best-evidenced 4 for this specific Feature's requirements
(tenant-aware, backend-enforced, audit-integrated, enterprise-adopted).
