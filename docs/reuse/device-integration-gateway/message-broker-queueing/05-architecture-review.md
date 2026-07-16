# Architecture Review — Message Broker / Queueing

RabbitMQ's durable-queue + publisher-confirm model directly satisfies the
at-least-once delivery requirement already flagged twice elsewhere in
this program (Module 1's audit-hook pipeline, Module 3's immudb feed) —
one broker choice now retroactively firms up both of those Features'
"durable broker delivery required" notes. Kafka's log-retention model is
architecturally heavier than this platform's evidenced throughput needs
justify; NATS core's at-most-once default would need JetStream configured
correctly everywhere it matters, a higher misconfiguration-risk surface
than RabbitMQ's more explicit durability flags.
