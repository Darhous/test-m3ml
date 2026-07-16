# Risk Analysis — Tenant Provisioning

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Partial provisioning failure leaves an orphaned Keycloak Organization with no matching tenant partition (or vice versa) | Medium | Medium | Saga compensation steps + idempotent retry (Constitution Section 48) — an implementation-time design requirement, flagged here, not resolved |
