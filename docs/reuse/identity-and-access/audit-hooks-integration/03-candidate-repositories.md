# Candidate Repositories — Audit Hooks Integration

Not a separate-Engine Feature. The relevant capability is Keycloak's
built-in **Event Listener SPI** (custom event listeners can stream every
auth-relevant event to an external sink — message queue, webhook, log
pipeline). No alternative third-party repository evaluated — this is a
configuration/extension-point choice within the already-adopted Engine,
not a new Build-vs-Buy decision.
