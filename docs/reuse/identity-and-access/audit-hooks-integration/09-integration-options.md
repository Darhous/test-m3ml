# Integration Options — Audit Hooks Integration

Keycloak Event Listener SPI → platform-owned small adapter → message
broker (candidate TBD, see Device Integration Gateway Module) → Audit and
Compliance Module's immutable audit trail (candidate TBD, see that
Module's own research). This Feature's own decision is scoped to
confirming the SPI exists and is the correct extension point — the
downstream Engine choice belongs to the Audit and Compliance Module,
avoiding duplicate research per the Cross-Feature Dependency Map
discipline.
