# Architecture Review — Session Management

Keycloak's Admin Console and Admin REST API expose per-user active
session listing and forced-revocation ("Log out all sessions") — directly
usable for a Tenant Admin or Platform Operator responding to a
compromised-account scenario without custom session-store engineering.
Session data is held server-side (Keycloak's own store, backed by its
configured database/cache), not merely client-side JWT expiry — a
meaningful architectural advantage for true forced-logout capability.
