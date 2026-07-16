# Risk Analysis — Authorization (RBAC/ABAC)

| Risk | Likelihood | Impact | Mitigation | Cross-Reference |
|---|---|---|---|---|
| Rego's learning curve slows the team writing/reviewing the actual Result Verification policy rules correctly | Medium | Medium-High (a wrong policy rule has direct clinical-safety impact, per Risk Register #20/SEC-07) | Policy rules should get the same review rigor as the business rule itself (Wave 6) — an SAD/implementation-time process decision, not resolved here | Risk Register #20 (Highest severity) |
| Two authorization engines (Keycloak RBAC + OPA ABAC) creates a coordination/consistency risk if their views of a user's attributes drift | Low-Medium | Medium | OPA should source attributes from the same Keycloak-issued token/claims as RBAC, not a separately-synced copy, to avoid drift | `09-integration-options.md` |
| OPA policy bundle deployment/versioning mismanaged, causing a stale policy to evaluate a live decision | Low | High (clinical-safety-adjacent) | OPA's own bundle-versioning and signed-bundle features should be used, not a custom distribution mechanism — an SAD-level configuration decision | `13-upgrade-strategy.md` |

## Overall Risk Rating

**Medium-High** — not because OPA itself is risky (it scored the highest
of any candidate in this Module), but because this Feature sits directly
on top of the single highest-priority Open Question in the entire
Discovery program (`open-questions.md` #19, Result Verifier eligibility)
and the Highest-severity Risk Register entry tied to it (#20). The Engine
choice reduces implementation risk; it cannot resolve the underlying
business-rule uncertainty.
