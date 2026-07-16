# Global Search Log — Message Broker / Queueing

**Query:** `RabbitMQ vs Kafka vs NATS message broker durable delivery
2026 comparison`

**Findings:** Kafka — disk-based persistence, event-streaming/analytics
scale (1M+ msg/s), overkill for this platform's evidenced scale (Risk
Register #1, no measured need). NATS core — at-most-once by default
(JetStream adds durability but is a newer, less battle-tested layer).
**RabbitMQ** — "balances these extremes with configurable persistence and
acknowledgment patterns," durable queues + persistent messages + publisher
confirms give real at-least-once guarantees, best fit at this platform's
"moderate scale (10K-100K msg/s)" per independent 2026 sources.
