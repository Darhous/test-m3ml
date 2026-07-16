# Risk Analysis — Tenant Configuration

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Unleash's payload model proves too limited for a genuinely complex config need not yet anticipated | Medium | Low-Medium | The BUILD fallback already exists in this decision — not a hard dependency on Unleash's payload richness alone |
| Config split across two mechanisms (Unleash payloads + platform table) creates confusion about which one governs a given setting | Low-Medium | Low | Needs a clear, documented boundary rule at implementation time (SAD-level), flagged here |
