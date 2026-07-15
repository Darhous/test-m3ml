# Playbook 03 — Event Storming

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 2 of 11 domain-content phases
**Depends On:** Playbook 02 (Business Capability Map and Value Streams exist)
**Produces For:** Playbook 04 (Domain Discovery clusters these events into
candidate subdomains), Playbook 05 (Domain Modeling drafts Aggregates from
the events/commands surfaced here), Playbook 08 (Integrations Discovery
uses the External System touchpoints surfaced here)

---

## Purpose

Run a Big-Picture Event Storming pass across every Value Stream from
Playbook 02, surfacing the raw material of the domain: Domain Events (past
tense, business-meaningful), the Commands that trigger them, the Actors who
issue those commands, External Systems that participate, and Hotspots
(points of confusion, disagreement, or missing information). This is
deliberately messy and exhaustive — organizing the mess into subdomains is
Playbook 04's job, not this one's.

## Scope

**In scope:** eliciting and chronologically ordering Domain Events across
each Value Stream, identifying Commands/Actors/External Systems/Hotspots,
naming events in Ubiquitous Language consistent with Constitution Section
6/12/13's naming conventions.

**Out of scope:** clustering events into subdomains (Playbook 04), defining
Aggregates (Playbook 05), defining Bounded Context boundaries (Playbook 06),
finalizing Integration Event schemas (that is Playbook 06/07's job, once
contexts exist — this phase produces *candidate* event names only).

## Inputs

- `docs/discovery/artifacts/02-business-capability-map.md`
- `docs/discovery/artifacts/02-value-streams.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 6 (DDD Rules), Section
  12–13 (Event-Driven Architecture Rules, Event Naming)

## Preconditions

- Playbook 02 marked complete in the execution ledger.
- At least one Value Stream exists to storm.

## Required Skills

- `domain-driven-design` — specifically its Domain Events framework section
  (naming, "what the domain cares about," internal-vs-integration
  distinction primer, even though the internal/integration split is
  formalized later in Playbook 06).
- `mermaid-diagrams` — to render the storming board as a timeline/sequence
  representation for later phases to consume.

## Required Context Files

`glossary.md` (existing Draft Ubiquitous Language terms — reuse them, don't
invent synonyms), `vision.md`.

## Project Bindings (this project)

- Every event surfaced here that touches Laboratory workflows should be
  checked against Constitution Section 24/25 (Medical Device Integration,
  Workflow Rules) once External Systems/Actors implicate a device or a
  multi-step approval — flag, do not resolve, at this phase.

## Execution Steps

1. For each Value Stream from Playbook 02, walk it step by step and elicit
   every Domain Event that occurs — named in past tense, business language
   (e.g., `SampleCollected`, `ResultVerified`), per Constitution Section 12.
2. For each event, identify: the Command that triggered it (if any — some
   events are triggered by time or by another event, not a command), the
   Actor who issued the command (a Role from `glossary.md` if one exists,
   or a new candidate Role), and any External System involved (device,
   payer, partner lab, regulatory body).
3. Order events chronologically per Value Stream on the storming board.
4. Mark every Hotspot explicitly: a point where the business logic is
   unclear, contested, or unknown. A Hotspot is a first-class output, not a
   failure of the exercise.
5. Identify Pivotal Events: events that mark a significant business-state
   transition or a handoff between stakeholder groups (these become strong
   candidates for Bounded Context boundaries in Playbook 06 — flagged here,
   decided there).
6. Do not resolve a Hotspot by guessing during this phase — log it and move
   on; Hotspots feed `open-questions.md` (via the phase report) if they
   remain unresolved by Playbook 11 (Validation).

## Deliverables

- A chronologically ordered Event Storming board per Value Stream: Events,
  Commands, Actors, External Systems, Hotspots, candidate Pivotal Events.

## Produced Artifacts

- `docs/discovery/artifacts/03-event-storming-board.md` (one section per
  Value Stream)
- `docs/discovery/reports/03-event-storming-report.md` (Hotspot list,
  Pivotal Event candidates, Actor/External System inventory)

## Required Diagrams

- One Mermaid `sequenceDiagram` or timeline-style `flowchart` per Value
  Stream, showing Actor → Command → Event chains and External System
  touchpoints, stored under `docs/discovery/diagrams/`.

## Review Checklist

- [ ] Every event name is past tense and in Ubiquitous Language (no
      `Manager`/`Helper`/`Processor`/`Utils`-style names, per Constitution
      Section 6).
- [ ] Every event traces back to a Value Stream from Playbook 02 — no
      orphan events invented outside a traced flow.
- [ ] Every Hotspot is recorded with enough context that a later phase can
      act on it without re-running this session.
- [ ] Pivotal Events are marked as *candidates* only, not decided Bounded
      Context boundaries.

## Quality Gates

- **Naming Gate:** every event name checked against Constitution Section 6
  (DDD naming) and Section 40 (Naming Conventions) before being accepted
  onto the board.
- **No-Silent-Resolution Gate:** a Hotspot may not be closed within this
  phase by an assumption — it is either resolved by an explicit user
  answer, or it remains open and is carried forward.

## Exit Criteria

- Every traced Value Stream has a complete, chronologically ordered event
  chain with Actors and External Systems identified.
- Every Hotspot is logged in the phase report.
- Candidate Pivotal Events are identified and handed to Playbook 04/06.

## Files To Update

- `.claude/context/glossary.md` — append newly surfaced Ubiquitous Language
  terms (events, actor/role candidates) as `Draft`, reusing existing terms
  where they already exist rather than duplicating.
- `.claude/context/open-questions.md` — append any Hotspot that is a
  genuine open business/domain question (not a modeling detail to be
  resolved in Playbook 05/06).

## ADR Impact

None expected — Event Storming is pre-decision, raw material gathering. A
Pivotal Event revealing a *structural* implication (e.g., "this looks like
it needs to cross a tenant boundary in a new way") is flagged for Playbook
06/09, not resolved with an ADR here.

## Common Mistakes

- Naming events after CRUD operations (`RecordCreated`, `RecordUpdated`)
  instead of business-meaningful facts (`ResultVerified`) — a direct
  violation of Constitution Section 6's DDD naming rule.
- Trying to resolve Hotspots during the storming session instead of
  recording and moving on (kills the exercise's momentum and biases later
  phases toward whatever answer was guessed under pressure).
- Conflating a Domain Event with an Integration Event this early — that
  distinction is Playbook 06's job (Constitution Section 12), not this
  phase's.
- Storming only the "happy path" and skipping failure/exception events
  (e.g., `SampleRejected`, `ResultDisputed`) — these matter as much as
  success events for later Business Rules (Playbook 07) work.

## Self Review

Walk the board chronologically per Value Stream and confirm it reads as a
coherent story a domain expert would recognize. Confirm every Hotspot has
enough written context to be actionable by someone who was not in the
storming session.

## Stop Conditions

- A Value Stream from Playbook 02 cannot be storm-walked because its steps
  are too vague — return to Playbook 02 for that specific stream rather
  than inventing events to fill the gap.
- An event is proposed that only makes sense if an Accepted Constitution
  rule or ADR is violated (e.g., an event implying AI silently finalizes a
  diagnosis) — stop, do not add it to the board, flag as a Conflict per
  `EXECUTION-GUIDE.md`.
