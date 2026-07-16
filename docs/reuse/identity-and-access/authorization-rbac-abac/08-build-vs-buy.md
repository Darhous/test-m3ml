# Build vs. Buy — Authorization (RBAC/ABAC)

| Dimension (Weight) | OPA | Casbin | Keycloak Auth. Services | Build In-House |
|---|---|---|---|---|
| Architecture (15%) | 5 — purpose-built for this exact problem shape | 4 — simpler, slightly less expressive for deep nesting | 3 — real but not designed for this depth | 2 |
| Security (15%) | 5 — CNCF Graduated, formal audit history | 4 | 4 (inherits Keycloak) | 1 — a Sensitive-Operation-grade policy engine is exactly the kind of thing not to build from scratch |
| License (10%) | 5 | 5 | 5 | 5 |
| Testing/CI (10%) | 5 | 4 | 4 | 1 |
| Community Health (10%) | 5 | 4 | 4 (shared with authentication) | N/A |
| Enterprise Adoption (10%) | 5 | 4 | 3 for this specific sub-feature | 0 |
| Healthcare Suitability (10%) | 4 — general-purpose, proven fit for structured multi-attribute rules like the Policy Model | 4 | 3 | Unknown |
| Documentation (5%) | 4 — Rego has a real learning curve documented at length | 5 — simpler model, easier docs | 4 | Unknown |
| Extensibility (5%) | 5 | 4 | 3 | 5 (at full cost) |
| Upgradeability (5%) | 4 | 4 | 4 | Unknown |
| Vendor Independence (5%) | 5 — CNCF | 5 — no single vendor | 5 (shared) | 5 |

**Weighted totals:** OPA **4.7**, Casbin **4.1**, Keycloak Authorization
Services **3.6**, Build In-House **~1.6**.

## Conclusion

**OPA wins on architecture, security governance, and enterprise
adoption** — specifically because the Configurable Result Verification
Policy Model's 8-dimension, Sensitive-Operation-grade, Audit-required
shape is precisely the problem OPA/Rego was designed to solve, and its
CNCF Graduated status gives it the strongest security-governance signal
of any candidate found in this entire Module so far.
