# Risk Analysis — Audit Hooks Integration

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Event listener misconfigured/disabled, silently creating an Audit gap | Low-Medium | High (undermines Constitution Section 23's immutability guarantee, ties to Risk Register #25/SEC-13) | Health-check/heartbeat monitoring on the listener pipeline itself — an SAD-level operational decision, flagged here so it is not silently assumed always-on |
| Message broker unavailability causes lost (not just delayed) audit events if forwarding is fire-and-forget | Medium | High | Broker choice (Device Integration Gateway Module) must support durable/at-least-once delivery for this specific use, not just best-effort |
