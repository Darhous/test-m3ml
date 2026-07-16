# Master Comparison Matrix

Per-Feature weighted-score comparison across all candidates evaluated.
Scoring model (each dimension 0–5, explained per candidate in that
Feature's own `07-community-review.md`/`06-security-review.md`/etc. —
not re-derived here):

**Weights:** Architecture 15%, Security 15%, License 10%, Testing/CI 10%,
Community Health 10%, Enterprise Adoption 10%, Healthcare Suitability 10%,
Documentation 5%, Extensibility 5%, Upgradeability 5%, Vendor
Independence 5%. GitHub star count is explicitly **not** a scoring
dimension (program instruction) — it may appear in the narrative as
context only.

Populated per Module as research completes.

| Module | Feature | Candidate | Weighted Score | Recommendation |
|---|---|---|---|---|
| Identity and Access | authentication | Keycloak | 4.6 | **Selected** |
| Identity and Access | authentication | Authentik | 3.5 | Not selected |
| Identity and Access | authentication | Ory | 3.5 | Not selected |
| Identity and Access | authentication | Zitadel | 3.3 | Not selected (AGPL) |
| Identity and Access | authentication | Build In-House | ~1.5 | Rejected |
| Identity and Access | authorization-rbac-abac | OPA | 4.7 | **Selected** |
| Identity and Access | authorization-rbac-abac | Casbin | 4.1 | Not selected (close second) |
| Identity and Access | authorization-rbac-abac | Keycloak Authorization Services | 3.6 | Not selected |
| Identity and Access | authorization-rbac-abac | Build In-House | ~1.6 | Rejected |
| Tenant and Organization Management | feature-flags | Unleash | 4.5 | **Selected** |
| Tenant and Organization Management | feature-flags | Flagsmith | 4.0 | Not selected (close second) |
| Tenant and Organization Management | feature-flags | Build In-House | ~1.7 | Rejected |
