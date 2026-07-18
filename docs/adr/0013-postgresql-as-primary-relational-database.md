# 0013: PostgreSQL as the Primary Relational Database

## Status

**Accepted (Pre-SAD Baseline Correction, 2026-07-18).**

## Context

Every accepted Baseline entry and ADR that touches persistent
transactional data already assumes PostgreSQL-specific capabilities
without ever stating PostgreSQL itself as a formal, standalone
decision:

- **Row-Level Security (RLS)** is the ratified shared-tier
  partitioning mechanism for Hybrid Tenant Isolation (ADR-0005,
  confirmed via the Open Questions Resolution phase, D-42) — RLS is a
  PostgreSQL-native feature, not a generic relational-database
  capability.
- **`pgvector`** (Technology Baseline L1, PostgreSQL License) is a
  ratified Library, itself a PostgreSQL extension with no meaning
  outside a PostgreSQL instance.
- **Reference Standard R4** in `docs/architecture-review/
  02-TECHNOLOGY-BASELINE.md` is literally named "PostgreSQL Row-Level
  Security" and adopted by reference.
- **Schema per Module** (ADR-0003, Accepted) is written in
  database-agnostic language but every Module's actual reuse research
  (`docs/reuse/`) and every Engine in the Technology Baseline that
  owns its own transactional store (ERPNext, Frappe HR, Kill Bill,
  openIMIS, OpenBoxes) is documented running against PostgreSQL in its
  own upstream deployment guidance.

This gap was identified, not invented, by `23-SAD-READINESS-MATRIX.md`
(Data Architecture row, "Partially Ready") during the Architecture
Readiness Review — the substance was never in doubt, only the formal
statement was missing. This ADR closes that gap.

## Decision

**PostgreSQL is the primary transactional relational database engine
for the platform's Version 1 architecture.**

This is the authoritative default relational engine for transactional
Module data (per-Module owned schemas, ADR-0003) unless a future ADR
approves a specific exception for a specific workload.

## What This Decision Does Not Mean

- **Not every workload must be stored in PostgreSQL.** Analytics
  warehousing (Apache Superset, E10, already may read from
  purpose-built aggregates), search indices, object/document storage
  (Alfresco, E11; Documenso, E12), caches, and the event broker
  (RabbitMQ, E7) are explicitly out of this ADR's scope — those are
  already independently decided (or left open) elsewhere and are not
  retroactively pulled under this ADR.
- **Not every Module shares one physical database instance.** Schema
  per Module (ADR-0003) and Hybrid Tenant Isolation (ADR-0005) both
  already establish that a "shared PostgreSQL default" is compatible
  with per-Module schema boundaries and per-Tenant dedicated
  deployments (the Dedicated tier may run its own PostgreSQL instance
  entirely, still consistent with this ADR).
- **Not a hosting or managed-service decision.** Whether a given
  environment runs self-hosted PostgreSQL, a managed cloud PostgreSQL
  service, or an on-premise instance is a deployment-topology decision
  (ADR-0009's replaceable-cloud-provider principle applies), not an
  engine decision — that stays open, correctly, for the SAD/
  Implementation phase to decide per deployment.

## Rationale

1. **Already the de facto choice, made explicit rather than invented.**
   Every PostgreSQL-specific capability cited in Context is already an
   Accepted or ratified artifact — this ADR does not select a new
   technology, it names the technology every existing decision already
   depends on. This is the same "convert an implicit answer into an
   explicit decision" pattern already used throughout the Open
   Questions Resolution phase.
2. **RLS is the ratified tenant-isolation mechanism (D-42).** Rendering
   RLS achievable requires PostgreSQL specifically — no other
   relational engine implements row-level security in a functionally
   equivalent way compatible with the Hybrid Tenant Isolation design
   already Accepted.
3. **`pgvector` is a ratified Library with no meaning without
   PostgreSQL.** Leaving the underlying engine formally undecided while
   a PostgreSQL-only extension is already ratified is the exact kind of
   inconsistency this ADR resolves.
4. **License and maturity profile match this project's demonstrated
   pattern.** PostgreSQL License (permissive, BSD-style) is consistent
   with the Technology Baseline's repeatedly-demonstrated preference
   for permissive licenses (Apache-2.0/MIT/PostgreSQL License account
   for the large majority of ratified Engines and Libraries).

## Consequences

### Positive

- Closes the one Data Architecture gap `23-SAD-READINESS-MATRIX.md`
  identified — that section moves from Partially Ready to Ready once
  this ADR is cited.
- Gives every Module team a single, unambiguous default; no Module
  needs to independently justify "why PostgreSQL" going forward.
- Confirms RLS and `pgvector` were sound choices resting on a real
  engine decision, not an implicit assumption that could have silently
  diverged Module-by-Module.

### Negative

- None identified beyond the ordinary cost of a relational-engine
  standardization: any future workload with a genuine non-relational or
  non-PostgreSQL-suited access pattern must justify an explicit
  exception rather than defaulting silently.

## Constraints

- A Module's schema (ADR-0003) is a PostgreSQL schema unless an
  approved exception states otherwise.
- Row-Level Security (D-42) requires this decision to hold — reversing
  this ADR without a coordinated replacement for D-42 would break the
  ratified tenant-isolation mechanism.
- `pgvector` (Technology Baseline L1) requires this decision to hold
  for the same reason.

## Alternatives Considered

- **MySQL/MariaDB.** Rejected: no native Row-Level Security equivalent
  compatible with the already-Accepted RLS-based tenant isolation
  design (D-42); would require reopening ADR-0005's implementation
  detail, which this correction phase is explicitly not authorized to
  do.
- **A polyglot-persistence model with no default engine.** Rejected:
  leaving the default genuinely open (rather than PostgreSQL) is
  exactly the ambiguity this ADR exists to close; a "no default"
  position would also contradict the already-ratified RLS and
  `pgvector` decisions, which have no meaning without PostgreSQL.
- **A different vector-search-capable engine (e.g., a dedicated vector
  database) as the default.** Not considered as a *default engine*
  alternative — `pgvector`'s own Technology Baseline entry already
  notes a dedicated vector DB (Qdrant, Weaviate) as a Replacement
  Candidate "only if scale triggers it," i.e., an exception path this
  ADR's "unless a future ADR approves an exception" clause already
  accommodates, not a reason to withhold this default now.

## Reversibility and Exit Strategy

This decision is reversible via a new superseding ADR through
Constitution Section 45, consistent with every other ADR in this
repository. Because RLS-based tenant isolation and `pgvector` both
depend on PostgreSQL specifically, reversing this ADR is a coordinated
change, not an isolated one — a superseding ADR must also address
those two dependents explicitly, not leave them silently orphaned.

## Verification Requirements

- The SAD's Data Architecture section cites this ADR as the closure of
  the gap `23-SAD-READINESS-MATRIX.md` identified.
- Any future Module or Engine proposing a non-PostgreSQL transactional
  store must document the exception explicitly (Module README or a
  dedicated ADR), not adopt one silently.

## Relationship to Other Decisions

- **Tenant Isolation (ADR-0005, D-42)**: this ADR is the engine-level
  precondition for Row-Level Security's continued validity.
- **Schema per Module (ADR-0003)**: this ADR specifies which relational
  engine hosts each Module's schema by default.
- **Analytics**: out of scope — Apache Superset (E10) may read from
  PostgreSQL directly or from derived aggregates; this ADR does not
  mandate either.
- **Event persistence**: out of scope — RabbitMQ (E7) remains the
  event-transport Engine; whether event *history* is additionally
  persisted to PostgreSQL for replay/audit purposes is a SAD-level
  design decision this ADR does not pre-empt.
- **`pgvector` (Technology Baseline L1)**: this ADR is the engine-level
  precondition for `pgvector`'s continued validity, as described above.
