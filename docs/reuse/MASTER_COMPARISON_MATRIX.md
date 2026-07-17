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
| Audit and Compliance | immutable-audit-trail | immudb | 4.5 | **Selected** |
| Audit and Compliance | immutable-audit-trail | Trillian | 3.9 | Not selected |
| Audit and Compliance | immutable-audit-trail | Build (Postgres append-only) | ~2.2 | Rejected |
| Audit and Compliance | compliance-tracking | Eramba | 3.6 | **Selected (tentative)** |
| Audit and Compliance | compliance-tracking | CISO Assistant | 3.4 | Close second |
| Audit and Compliance | compliance-tracking | GovReady-Q | 3.1 | Not selected |
| Audit and Compliance | compliance-tracking | Build In-House | ~1.8 | Rejected |

**Scope note (final, honest disclosure):** Full numeric weighted-scoring
tables at this granularity were maintained for Modules 1-3 only. After
the user's mid-program pacing instruction to proceed at a "not too deep,
not shallow" depth for the remaining 25 Modules, per-candidate numeric
scores were not fabricated retroactively to fill this table — doing so
would violate the No-Guessing Rule (a score implies a rigor of
comparison that was not actually performed at that granularity for
Modules 4-28). Every Module's actual comparative reasoning (why one
candidate was chosen over another) is fully documented in narrative form
in each Feature's own `03-candidate-repositories.md` and
`08-build-vs-buy.md` files, and in `MASTER_DECISION_REGISTER.md`'s
106-row rationale column — that is the authoritative comparison record
for Modules 4-28, not a numeric score reconstructed after the fact.
