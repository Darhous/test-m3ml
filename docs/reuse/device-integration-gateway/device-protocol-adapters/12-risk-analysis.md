# Risk Analysis — Device Protocol Adapters

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Each new vendor integration silently bypasses the shared normalization/idempotency pattern | Medium | Medium | Enforce the adapter pattern as a Module 8 (Device Integration Gateway) code-review standard, not left to individual integration authors |
