# Final Decision — Audit Hooks Integration

## Decision: **LIBRARY** (thin platform-owned adapter over Keycloak's
built-in Event Listener SPI)

Not an Engine decision — the SPI is a configuration/extension point
within the already-adopted Keycloak Engine. The adapter code itself is
necessarily platform-specific glue (small, owned, not a reuse candidate)
and is classified as a Library-scale build, not a new external Engine.
