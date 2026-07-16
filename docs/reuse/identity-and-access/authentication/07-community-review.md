# Community and Adoption Review — Authentication

| Candidate | Governance | Enterprise Adoption Signal | Maintenance Cadence |
|---|---|---|---|
| Keycloak | CNCF Incubating project; primary corporate steward Red Hat/IBM (also ships as "Red Hat build of Keycloak") | Explicitly cited in search results as deployed in regulated industries including finance and healthcare; used in production by thousands of organizations for years | Monthly point releases (26.5.4 → 26.5.6 → 26.5.7 across Feb–April 2026 alone) |
| Zitadel | Company-led (ZITADEL GmbH), open-core commercial model | Growing SaaS/cloud-native adoption; newer, thinner independent-verification trail of large regulated-industry deployments than Keycloak | Regular release cadence, single-binary simplicity aids operational maturity |
| Authentik | Company-led (Authentik Security), open-core | Strongest in self-hosting/homelab/SME segment per search results; less evidence of large regulated-industry (healthcare-scale) production deployment than Keycloak | Frequent releases |
| Ory | Company-led (Ory Corp) | Hydra's OpenID Foundation certification is a strong protocol-conformance signal; adoption is real but more fragmented across the multiple separate services | Active per-service release cadence |

## Long-Term Sustainability

Keycloak carries the lowest single-vendor risk of the 4: CNCF governance
means the project does not depend solely on one company's continued
existence, and IBM's acquisition of Red Hat gives it the deepest
corporate backing among the candidates. This directly serves the
program's "Vendor Independence" scoring dimension.
