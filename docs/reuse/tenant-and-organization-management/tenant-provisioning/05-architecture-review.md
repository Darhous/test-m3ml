# Architecture Review — Tenant Provisioning

Provisioning is inherently a **Saga** (multi-step, cross-system
workflow: create Keycloak Organization → create tenant partition/record
→ create initial admin user → send welcome notification via the
Notification Service, researched separately) — this is Discovery Wave
5's own event-chain modeling territory (Domain Events), not a reuse-
research question. This Feature's contribution is confirming the
building blocks (Keycloak Admin API, RLS tenant record) exist and are
already selected, so the Saga's steps call proven Engines, not custom
per-step integrations.
