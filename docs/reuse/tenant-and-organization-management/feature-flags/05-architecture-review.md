# Architecture Review — Feature Flags

| Dimension | Unleash | Flagsmith |
|---|---|---|
| Governance features | Change-request 4-eyes approval, granular RBAC, full audit logging — directly reusable for gating any future "Elevated Audit tier" feature rollout (Wave 6 candidate) | Real-time propagation (vs. polling), server-side identity/trait storage — lower per-evaluation overhead |
| OpenFeature support | Yes | Yes (founding member — deepest native support) |
| Remote configuration (beyond boolean flags) | Supported | Explicitly combines toggles + remote config as a core design goal — directly serves `tenant-configuration` Feature (see that Feature's files) |
| Fit for Plan/Entitlement gating (SaaS Commercial Operations Module) | Strong — RBAC and audit trail suit a billing-adjacent gate | Strong — remote-config model suits per-Plan configuration values, not just on/off flags |

## Assessment

Both are architecturally strong; the differentiator is **Unleash's
built-in change-approval governance** (directly reusable for Sensitive/
Elevated-Audit-tier feature rollouts, Constitution Section 21-adjacent)
versus **Flagsmith's unified flags+config model** (directly reusable for
the separate `tenant-configuration` Feature, avoiding a second engine
there — see `MASTER_DEPENDENCY_MATRIX.md`).
