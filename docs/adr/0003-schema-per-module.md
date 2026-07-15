# 0003: Schema per Module

## Status

Accepted

## Context

Given Modular Monolith First (ADR 0001) and Domain-Driven Design (ADR
0002), each module owns one or more Bounded Contexts and must remain
extractable later without a data-layer rewrite. A single shared database
schema used freely by all modules would let any module read/write any other
module's tables, silently destroying the module boundaries the other two
decisions establish. At the same time, requiring a fully separate database
per module from day one is not justified yet — no measured operational
need for that exists (many scale-related questions remain `Open`).

## Decision

Inside the initial Modular Monolith, **every module owns a distinct schema
(or clearly namespaced table set) and its own migrations**. No module may
read or write another module's tables directly. Cross-module data access
happens only through APIs, Domain/Integration Events, or approved Read
Models. Database per Module is not required initially; a module may move to
a fully separate database when/if it is extracted into an independent
service (ADR 0001), and large/regulated tenants may receive a dedicated
database as a deployment-topology choice (ADR 0005), independent of this
module-boundary decision.

## Alternatives Considered

- **One shared schema, no per-module boundary.** Rejected: fastest to start
  but guarantees the Modular Monolith degrades into a Distributed-Monolith-
  in-waiting, since nothing stops direct cross-module joins.
- **Database per Module from day one.** Rejected for v1: adds migration/
  transaction/operational complexity (e.g., no cheap cross-module
  transactions) before any measured need forces it; conflicts with
  "do not over-engineer infrastructure prematurely" (Constitution Section
  "Scalability").
- **Schema per Module inside one database.** **Chosen.** Enforces the
  ownership boundary (via schema separation and DB permission grants)
  without paying full database-per-module operational cost yet, and keeps
  the door open to Database per Module later per module, as needed.

## Positive Consequences

- Module ownership of data is enforceable today via database permissions,
  not just code review discipline.
- A module can be extracted to its own database later as a pure deployment
  change, since it never depended on cross-schema access.
- Keeps v1 operationally simpler (one database to run/back up/monitor).

## Negative Consequences

- Cross-module reporting/analytics queries cannot use simple SQL joins
  across schemas; they must go through approved Read Models or the
  Analytics Platform (Independent Component).
- Some short-term convenience is sacrificed for long-term module integrity.

## Risks

- **Silent boundary violation**: a developer adds a cross-schema query
  under time pressure. Mitigated by database permission checks and
  repository dependency tests (Constitution Section 16), not code review
  alone.
- **Migration ordering issues** if migrations are run without respecting
  the module dependency graph. Mitigated by per-module migration ownership
  and CI dry-run checks (Constitution Section 17).

## Verification

- Database role/grant configuration restricting each module's DB credential
  to its own schema.
- Repository/ORM-layer dependency tests forbidding cross-schema access.
- Migration ownership check: migrations live under the owning module's
  directory.

## Revisit Triggers

- A specific module demonstrates a measured need for full Database per
  Module (e.g., independent scaling, extraction, or a regulated-tenant
  dedicated-database requirement) — handled per-module, not as a reversal
  of this ADR.
- Analytics/reporting needs outgrow the approved-Read-Model approach,
  prompting a dedicated Analytics Platform design (already anticipated as
  an Independent Component).
