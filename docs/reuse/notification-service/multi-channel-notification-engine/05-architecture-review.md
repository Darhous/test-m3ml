# Architecture Review — Multi-Channel Notification Engine

Novu's workflow model (trigger → subscriber preferences → channel
fan-out) fits Constitution Section 11's Independent Component pattern
directly — the platform calls Novu's API with a notification-intent
event, Novu owns channel-specific delivery mechanics. Self-hosted
deployment requires MongoDB + Redis + Novu's own services — additional
operational components beyond the platform's already-selected
PostgreSQL/RabbitMQ stack, a real integration-cost note, not a blocker.
