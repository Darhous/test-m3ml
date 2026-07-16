# Build vs. Buy — Audit Hooks Integration

Not an independent Build-vs-Buy decision — this Feature is the
integration glue between two already-decided Engines (Keycloak, and the
Audit and Compliance Module's own audit-trail engine, researched
separately). The "build" here is intentionally small and platform-owned
(the event-forwarding adapter itself), consistent with Constitution
Section 8's One Owning Module rule — this thin glue code is not a
candidate for third-party reuse and is correctly excluded from the
Engine/Library/SDK classification.
