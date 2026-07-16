# Risk Analysis — Message Broker / Queueing

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Broker becomes a single point of failure for every downstream durability guarantee (audit, device data) | Medium | High | RabbitMQ clustering/mirrored-queue configuration — an SAD/operational decision, flagged not resolved |
| Broker throughput needs eventually exceed RabbitMQ's comfortable range | Low (no measured need yet, Risk #1) | Medium | Revisit Kafka only if a real measured trigger emerges (Constitution Section 55), not preemptively |
