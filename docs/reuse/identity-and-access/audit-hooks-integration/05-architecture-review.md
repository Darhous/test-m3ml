# Architecture Review — Audit Hooks Integration

Event Listener SPI runs in-process within Keycloak and pushes events
synchronously or asynchronously to a configured destination. Recommended
pattern: publish to the platform's own message broker (see Device
Integration Gateway Module's `message-broker-queueing` Feature for the
broker candidate) rather than a direct point-to-point call to the Audit
and Compliance Module, preserving loose coupling (Constitution Section
7's Published Language / Open Host Service pattern) and resilience if the
Audit Module is briefly unavailable.
