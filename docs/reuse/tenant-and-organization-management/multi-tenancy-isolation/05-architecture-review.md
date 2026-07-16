# Architecture Review — Multi-Tenancy Isolation

## Fit Against ADR 0005 and Risk #17

RLS enforces tenant filtering **inside the database engine itself**, at
the query-planner level — meaning even a buggy application-layer query
that forgets a `WHERE tenant_id = ...` clause still cannot leak
cross-tenant rows, because the database silently applies the RLS policy
regardless. This is architecturally the strongest available mitigation
for Risk #17's actual failure mode ("cross-tenant data leakage via the
shared-tier isolation mechanism") of any option reviewed — stronger than
relying on application-layer discipline alone, and far less operationally
costly than schema-per-tenant at this platform's evidenced scale (no
Confirmed tenant-count/volume numbers exist yet — Risk Register #1 — so
"evidenced scale" here means "no measured need for schema-per-tenant's
extra isolation has been demonstrated," not a specific number).

## Composition With Keycloak Organizations (Module 1)

RLS's `tenant_id` and Keycloak's Organization ID are the same logical
concept expressed in two systems — the platform's own Identity and
Access Adapter (Module 1) should propagate the authenticated user's
Organization ID into the database session's RLS context variable on every
request, closing the loop between "who is this user" (Keycloak) and
"what can they see" (Postgres RLS). This is a genuine, evidence-based
architectural connection this program's research surfaced between two
independently-researched Features.
