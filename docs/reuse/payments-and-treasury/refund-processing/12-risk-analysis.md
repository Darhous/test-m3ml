| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Gateway-side refund succeeds but ledger-side Credit Note fails (or vice versa), leaving an inconsistent state | Low-Medium | Medium | Idempotent, 2-phase composition with reconciliation checks, an implementation-time design requirement |
