# Risk Analysis — Multi-Channel Notification Engine

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| License terms turn out unfavorable once verified | Low-Medium | Medium | `Requires Legal Verification` before commitment; Courier/Knock remain fallback SaaS options if self-hosting proves unviable |
| Notification payload over-discloses clinical information | Medium | Medium-High (privacy) | Minimize payload content, require in-Portal login for detail (Constitution Section 30) |
| Added operational stack (MongoDB, Redis) beyond platform's PostgreSQL/RabbitMQ baseline | Medium | Low-Medium | Real but modest operational cost, not a blocker |
