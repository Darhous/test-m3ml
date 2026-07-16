# Architecture Review — Authorization (RBAC/ABAC)

| Dimension | OPA | Casbin | Keycloak Authorization Services |
|---|---|---|---|
| Deployment | Separate service/sidecar (or library) | In-process library, no separate service | Part of the already-running Keycloak service |
| Policy language | Rego (declarative, purpose-built, real learning curve) | Simple `.conf` model + policy files/DB rows, lower learning curve | UMA 2.0 policies configured via Keycloak Admin Console/API |
| Fit for 8-dimension context-aware Result Verification Policy | Strong — Rego is designed exactly for "evaluate a decision against many structured input attributes," matching the 8-dimension model closely | Strong — ABAC mode supports attribute matching; simpler but less expressive for deeply nested conditional logic | Weaker — UMA's resource/scope/policy model is real but was not designed for this level of multi-dimensional business-rule expressiveness; would likely require significant custom policy-provider code, eroding the "engine, not build" benefit |
| Operational footprint | Adds one more deployed component (or embeds as a Go library, less natural for a mixed-language platform) | Zero extra deployed component if used as an in-process library in the platform's own service language | Zero extra component — already running |
| Auditability of decisions | Strong — OPA decision logs are a first-class, well-documented feature, directly serving Constitution Section 23 (Audit) | Requires the adopting application to log decisions itself (Casbin does not natively provide decision-audit logging) | Inherits Keycloak's own audit event stream |

## Assessment

OPA's Rego language and native decision-logging are the strongest
architectural match for a Sensitive-Operation-grade, Audit-required,
multi-dimension policy (Constitution Section 21 + 23 + Wave 6's Policy
Model requirements together) — this is a genuine case where the "obvious"
answer (extend the already-adopted Keycloak) is architecturally weaker
than adding a second, purpose-built engine.
