# Multi-Tenancy

## Foundation

**Fact.** ADR-0005 (Hybrid Tenant Isolation) is Accepted: a two-tier
model — shared infrastructure with strict logical isolation for
small/medium tenants, dedicated database/deployment for large/
regulated tenants. This document applies that Accepted model to the
API layer specifically; it does not re-decide tenancy strategy.

## Tenant Isolation at the API Layer

Every API request carries tenant context in two independent places,
deliberately redundant for defense in depth:

1. **Token claim** — the authenticated identity's JWT includes Tenant
   ID (`08-AUTHENTICATION.md`), established at login and not
   caller-modifiable.
2. **`X-Tenant-Id` header** (`06-NAMING-CONVENTIONS.md`) — explicit,
   for the Routing Layer (`02-API-FIRST-ARCHITECTURE.md` Layer 2) to
   cross-check against the token claim. **A mismatch between the two
   is rejected outright (`403`), never silently resolved in favor of
   one or the other** — this is the concrete API-layer mechanism that
   makes cross-tenant leakage structurally hard, per this document
   set's stated Vision goal.

## API Isolation

- No API endpoint accepts a Tenant ID as a mutable request-body field
  for any operation that reads or writes data — Tenant scoping is
  always derived from authenticated context (above), never from
  client-supplied input, closing the most common cross-tenant leakage
  vector (a caller simply asking for another tenant's ID).
- Admin-classified APIs (`03-API-DOMAIN-INVENTORY.md`) that manage
  Tenants themselves (Tenant and Organization Management's Admin API)
  are the sole, explicit exception — and are further gated by an
  elevated Role plus the Break-Glass discipline where the action
  crosses tenant boundaries for support purposes.
- Rate limiting quotas (`13-RATE-LIMITING.md`) are tracked per-Tenant,
  so one Tenant's traffic volume cannot degrade another's service —
  isolation extends to availability, not only data.

## Data Isolation

Data isolation itself is governed by ADR-0005 and by the still-open
Open Question #15 (the exact shared-tier partitioning technology —
tenant-ID-column vs. schema-per-tenant; PostgreSQL Row-Level Security
is a logged Reference Standard, R4 in the Technology Baseline, but not
a resolution of #15). The API layer's role is narrower and does not
depend on #15's resolution: **every Module's Data-Scope PEP
(`09-AUTHORIZATION.md`) filters by Tenant regardless of which physical
partitioning scheme is eventually chosen** — the API contract and
authorization model are designed to be partitioning-technology-
agnostic, so #15's eventual resolution does not require an API-layer
redesign.

## Cross-Tenant Protection

- **Structural:** the token-claim/header cross-check above, plus
  Data-Scope filtering at every Module boundary, plus `404` (not
  `403`) on out-of-scope resource IDs (`05-API-STANDARDS.md`) to avoid
  confirming another tenant's resource even exists.
- **Auditable:** any successful cross-tenant access (necessarily
  Admin/Break-Glass, per the API Isolation rules above) is a mandatory
  Audit Event, consistent with `09-AUTHORIZATION.md`'s Break-Glass
  treatment.
- **Testable as a first-class concern:** the Quality Gates
  (`04-API-GOVERNANCE.md`) require an explicit multi-tenancy isolation
  check before any API reaches Published status — cross-tenant
  leakage is treated as a release-blocking defect class, not a
  post-hoc bug category.

## Organization and Branch Scoping

Below the Tenant level, the same pattern repeats for Organization and
Branch (per the project's own "organization/branch-based routing"
requirement, CLAUDE.md): Organization and Branch context are carried
in token claims, cross-checked against explicit request context where
provided, and enforced at the Module's Data-Scope PEP — the same
mechanism, applied recursively down the Tenant → Organization → Branch
hierarchy, rather than a separate mechanism per level.
