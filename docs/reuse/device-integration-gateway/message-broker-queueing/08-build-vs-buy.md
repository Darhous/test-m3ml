# Build vs. Buy — Message Broker / Queueing

| Dimension (Weight) | RabbitMQ | Kafka | NATS+JetStream | Build |
|---|---|---|---|---|
| Architecture (15%) | 5 — matches evidenced scale | 3 — over-scaled | 4 | 1 |
| Security (15%) | 4 | 4 | 4 | 1 |
| License (10%) | 5 | 5 | 5 | 5 |
| Community (10%) | 5 | 5 | 4 | N/A |
| Healthcare Suitability (10%) | 4 — durability-first fits audit/device criticality | 3 | 3 | Unknown |
| Vendor Independence (5%) | 3 — Broadcom-stewarded | 5 — ASF | 4 — CNCF | 5 |

**Weighted (approx):** RabbitMQ **4.4**, Kafka **3.9**, NATS+JetStream
**3.8**, Build **~1.6**.
