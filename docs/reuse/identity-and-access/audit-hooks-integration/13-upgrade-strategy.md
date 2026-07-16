# Upgrade Strategy — Audit Hooks Integration

The Event Listener SPI's interface is a stable, long-standing Keycloak
extension point across major versions — the adapter's exposure to
Keycloak upgrade churn is low relative to, e.g., Admin REST API surface
changes. No separate exit path needed beyond `../authentication/
13-upgrade-strategy.md`'s general Keycloak upgrade posture.
