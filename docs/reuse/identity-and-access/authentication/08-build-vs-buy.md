# Build vs. Buy Analysis — Authentication

## Weighted Enterprise Scoring (0–5 per dimension; weights per
`MASTER_COMPARISON_MATRIX.md`)

| Dimension (Weight) | Keycloak | Zitadel | Authentik | Ory | Build In-House |
|---|---|---|---|---|---|
| Architecture (15%) | 5 — mature SPI, proven at scale | 4 — modern event-sourced, less battle-tested | 4 — clean, modern | 3 — most flexible but most integration burden | 2 — unproven until built |
| Security (15%) | 4 — high scrutiny, active disclosure, but real recent CVEs | 4 — fewer disclosed CVEs but less scrutiny to interpret that from | 4 — same caveat as Zitadel | 4 — OIDC-certified core | 1 — auth is one of the hardest domains to build securely from scratch |
| License (10%) | 5 — Apache-2.0, Clear | 2 — AGPL-3.0, Conditional | 4 — MIT core, Conditional only for Enterprise tier | 5 — Apache-2.0, Clear | 5 — no license constraint |
| Testing/CI (10%) | 5 — extensive, CNCF-level rigor | 4 | 4 | 4 | 1 — would need to be built |
| Community Health (10%) | 5 — largest, most active | 3 | 3 | 3 | N/A |
| Enterprise Adoption (10%) | 5 — explicit healthcare/regulated-industry production use found | 3 | 2 | 3 | 0 |
| Healthcare Suitability (10%) | 4 — Organizations feature fits ADR 0005's Hybrid model | 4 | 3 | 3 | Unknown |
| Documentation (5%) | 5 | 4 | 4 | 3 — fragmented across services | Unknown |
| Extensibility (5%) | 5 — deep SPI | 3 | 3 | 4 | 5 (but at full build cost) |
| Upgradeability (5%) | 4 — frequent releases require active tracking | 4 | 4 | 4 | Unknown |
| Vendor Independence (5%) | 5 — CNCF governance | 2 — single-vendor, AGPL commercial lever | 3 — single-vendor, open-core | 4 | 5 |

**Weighted totals (approximate, out of 5):** Keycloak **4.6**, Zitadel
**3.3**, Authentik **3.5**, Ory **3.5**, Build In-House **~1.5** (most
dimensions score low or are simply undetermined pre-build).

## Effort Estimate If Built In-House

A production-grade authentication system covering password policy,
account lockout, credential storage (proper hashing/salting), brute-force
protection, and the login/logout lifecycle **alone** (before SSO, MFA, or
session management) is a well-documented multi-month effort for a
dedicated team even before accounting for the ongoing security-maintenance
burden this program's own Constitution (Section 21, 37) requires. No
specific hour figure is invented here (No-Guessing Rule) — the
qualitative conclusion (Build scores lowest across nearly every
dimension, particularly Security) is sufficient to support the decision
below without a fabricated number.

## Conclusion

**Buy/Reuse via Engine + Adapter: Keycloak.** Highest weighted score,
clearest license, strongest enterprise/regulated-industry adoption
evidence, and CNCF governance reducing vendor-lock risk. See
`10-final-decision.md`.
