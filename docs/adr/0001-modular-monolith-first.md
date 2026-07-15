# 0001: Modular Monolith First

## Status

Accepted

## Context

The platform starts with Laboratory Management and is intended to grow into
a broad, multi-domain healthcare platform (Identity, Organization, Patient,
Doctor/Clinic, Laboratory, Device Integration, Workflow, Notification,
Billing, Insurance, Inventory, AI/Analytics, Integration, Security/
Compliance, Support/Operations — see `.claude/context/module-catalog.md`
categories). At this stage, Bounded Contexts, team structure, and real
operational load are not yet known with confidence (many items remain
`Open` in `open-questions.md`, e.g., expected scale, hosting model,
market scope).

Two broad starting shapes were considered: begin as a set of independently
deployed microservices, or begin as a single deployable Modular Monolith
with clear internal Bounded Contexts.

## Decision

The platform starts as a **Modular Monolith**: one deployable unit
(excluding the explicitly named Independent Components — see 0006 and the
Constitution's Section 11) composed of modules aligned to Bounded Contexts,
with strict module boundaries enforced by contract (API/events), not by
network separation. Extraction of any module into an independent service
requires a documented, measurable operational or organizational trigger
(Selective Service Extraction), not a default expectation.

## Alternatives Considered

- **Microservices from day one.** Rejected: distributed-systems cost
  (network calls, partial failure, eventual consistency, deployment/
  operational overhead, cross-service transactions) is paid before the
  domain model, team structure, or load profile justify it. Team size and
  operational maturity are not established constraints supporting this yet.
- **Unstructured monolith (no enforced module boundaries).** Rejected:
  produces a Big Ball of Mud, which directly contradicts the "not a plain
  CRUD system" vision and would block later extraction entirely.
- **Modular Monolith with a few justified independent components.**
  **Chosen.** Balances low distributed-systems overhead with the specific,
  named cases (Section 11) where independence is already justified by
  concrete needs (protocol isolation, external-facing surface, variable
  load, governed external calls).

## Positive Consequences

- Lower operational complexity while the domain model and team structure
  are still being discovered.
- Module boundaries (contracts, no direct cross-module DB access) are
  enforced from the start, so extraction later is a deployment change, not
  a redesign.
- Faster iteration during the early, requirements-uncertain phase (many
  `Open Questions` remain).

## Negative Consequences

- Requires discipline (automated architecture tests) to prevent boundaries
  from eroding inside a single deployable.
- Some operational independence (e.g., independently scaling one module)
  is not available until that module is actually extracted.

## Risks

- **Boundary erosion risk**: without enforced tests, a Modular Monolith can
  silently become a Big Ball of Mud. Mitigated by Section 9 (Module
  Dependency Rules) automated tests as a Definition-of-Done gate.
- **Premature extraction risk**: teams may push to extract before a real
  trigger exists. Mitigated by requiring an ADR with a documented trigger
  before extraction (Constitution Section 5).

## Verification

- Architecture/dependency-direction tests confirming all module code lives
  in the single deployable except for the named Independent Components.
- No direct cross-module database access, verified via database permission
  checks and repository dependency tests (Constitution Section 16/17).

## Revisit Triggers

- A specific module shows a measured, sustained operational need for
  independent scaling, deployment cadence, or team autonomy that the
  Modular Monolith cannot satisfy.
- Organizational growth creates a team boundary that conflicts with the
  current module grouping.
- This decision is revisited per-module via Selective Service Extraction,
  not as a wholesale reversal of the Modular Monolith direction.
