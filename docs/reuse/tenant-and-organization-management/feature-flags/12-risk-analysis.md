# Risk Analysis — Feature Flags

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Flag evaluated with the wrong tenant context (cross-tenant feature leakage — a lower-severity cousin of Risk #17) | Low-Medium | Medium | Reuse the same Organization-ID propagation already relied on for RLS (`multi-tenancy-isolation`), not a separately-sourced identity |
| Over-reliance on flags as a substitute for real Entitlement enforcement (a flag is not itself a billing gate) | Medium | Medium | Feature flags and SaaS Commercial Operations' Entitlement engine (researched separately) must be architecturally distinct — flags control rollout, Entitlements control what a Plan actually grants — flagged here to avoid conflating them later |
