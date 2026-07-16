# Risk Analysis — Delivery Tracking

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Delivery-failure not surfaced to a clinically-time-sensitive notification (e.g., critical result alert) | Low-Medium | High (clinical) | Critical-result-class notifications need explicit failure-escalation handling, not silent drop — an implementation-time requirement |
