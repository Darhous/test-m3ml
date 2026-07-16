# Reusable Assets — Audit Hooks Integration

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| Workflow | Event-listener-to-broker-to-audit-sink pipeline shape | Keycloak Event Listener SPI pattern (industry-common usage) | Reusable pipeline shape for any future Module that needs to emit audit-relevant events, not just Identity and Access. |
