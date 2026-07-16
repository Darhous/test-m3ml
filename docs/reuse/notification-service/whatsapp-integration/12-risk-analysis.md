# Risk Analysis — WhatsApp Integration

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| WhatsApp Business API policy changes (Meta-controlled) disrupt delivery | Low-Medium | Medium | Novu's provider abstraction allows BSP swap without a platform-wide rewrite |
| Clinical detail over-disclosed in a WhatsApp message | Medium | Medium-High (privacy, Egypt PDPL) | Same payload-minimization discipline as `../delivery-tracking/` |
