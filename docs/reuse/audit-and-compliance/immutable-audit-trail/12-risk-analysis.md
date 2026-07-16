# Risk Analysis — Immutable Audit Trail

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| immudb itself becomes unavailable, blocking Sensitive Operations that require synchronous audit-write-before-proceed | Low-Medium | High (availability, Constitution Section 34) | Requires an explicit SAD-level decision on synchronous vs. asynchronous audit writes for Sensitive Operations — flagged, not resolved here |
| immudb's open-core model shifts a currently-OSS feature to Enterprise-only in a future release | Low | Medium | Track release notes; Trillian remains a credible fallback (see `10-final-decision.md`) |
| Broker-to-immudb pipeline (shared with Module 1's `audit-hooks-integration`) drops a message, creating a silent audit gap | Low-Medium | High (Risk #25) | Durable, at-least-once broker delivery required (already flagged in Module 1's Feature 12) |
