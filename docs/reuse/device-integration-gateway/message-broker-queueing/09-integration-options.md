# Integration Options — Message Broker / Queueing

Single RabbitMQ deployment, shared platform-wide as the durable-delivery
backbone: Device Integration Gateway → broker → downstream Modules;
Identity and Access's audit-hook pipeline (Module 1) → broker → Audit and
Compliance's immudb (Module 3). One broker, multiple topic/queue
bindings, not one broker per Module — a Shared Technical Service.
