# Playbook 05 — Domain Modeling (Candidate Pass)

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 4 of 11 domain-content phases
**Depends On:** Playbook 04 (candidate Subdomain map)
**Produces For:** Playbook 06 (Bounded Contexts formalizes boundaries around
these candidate Aggregates), Playbook 07 (Business Rules refines the
invariants sketched here)

---

## Note on Ordering (read before using this playbook)

This playbook runs *before* Playbook 06 (Bounded Contexts) deliberately.
The tactical building blocks drafted here (Aggregates, Entities, Value
Objects, candidate Domain Events) are **candidates** derived from the
Subdomain map, not final designs scoped to an already-fixed Bounded
Context. Playbook 06 then formally partitions these candidates into
Bounded Contexts and resolves any overlap or duplication this phase
surfaces. This mirrors the standard EventStorming-driven flow (Big Picture
→ Process/Design-Level modeling → Context crystallization) rather than the
textbook-order alternative (Bounded Contexts first, then tactical design
inside each). Both orders are legitimate DDD practice; this framework picks
the EventStorming-driven order because Playbook 03 already produced
process-level detail that would otherwise sit unused until Playbook 06.
**Do not skip Playbook 06's boundary-drawing on the assumption that this
phase already did it — it did not.**

## Purpose

Draft candidate Aggregates (with a single Aggregate Root each), Entities,
Value Objects, and refined Domain Events for each Subdomain identified in
Playbook 04, applying DDD tactical patterns (Constitution Section 6).

## Scope

**In scope:** candidate Aggregate boundaries, Entity vs. Value Object
classification, Aggregate Root identification, consistency-boundary
reasoning (what must be immediately consistent vs. eventually consistent),
refining Playbook 03's raw event names into proper Domain Events attached
to a specific Aggregate.

**Out of scope:** Bounded Context boundaries and Context Mapping patterns
(Playbook 06); fine-grained business rule/invariant text (Playbook 07 — this
phase identifies *that* an invariant exists and *where* it lives, not its
full detailed logic); Integration Event design (Playbook 06/07, since that
requires Bounded Context boundaries to exist first per Constitution Section
12).

## Inputs

- `docs/discovery/artifacts/04-subdomain-map.md`
- `docs/discovery/artifacts/03-event-storming-board.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 6 (Aggregates,
  Entities, Value Objects, Domain Events)

## Preconditions

- Playbook 04 marked complete; Subdomain map with Core/Supporting/Generic
  classification exists.

## Required Skills

- `domain-driven-design` — Entities/Value Objects/Aggregates and Domain
  Events sections specifically (the Entity test: "same thing even if all
  attributes change?"; the Value Object test: "defined only by
  attributes?").
- `mermaid-diagrams` — for Aggregate structure class diagrams.

## Required Context Files

`glossary.md` (reuse existing Draft terms for consistency).

## Project Bindings (this project)

- Every candidate Aggregate touching medical results or consent must be
  flagged for Constitution Section 21 (Data Scope) and Section 23 (Audit)
  applicability in Playbook 07 — this phase notes the flag, Playbook 07
  writes the actual rule.

## Execution Steps

1. For each Subdomain from Playbook 04, list the Entities/Value Object
   candidates implied by its events (an event like `ResultVerified` implies
   a `Result` concept with identity — likely an Entity or Aggregate Root).
2. Apply the Entity test and Value Object test from the
   `domain-driven-design` skill to each candidate; default to Value Object
   (immutable) unless the identity test clearly requires Entity status.
3. Group related Entities/Value Objects into candidate Aggregates, each
   with exactly one Aggregate Root, keeping aggregates small (Constitution
   Section 6: "one root plus the minimal cluster needed for its
   invariants").
4. For each Aggregate boundary decision, write a one-line consistency
   rationale: what must be immediately consistent inside this Aggregate,
   and why other related data is referenced by ID instead of embedded.
5. Attach refined Domain Events (from Playbook 03's raw list) to the
   specific Aggregate that raises them; rename any event whose Playbook-03
   name does not clearly attribute it to an Aggregate.
6. Flag every Aggregate that plausibly spans more than one Playbook-04
   Subdomain — this is exactly the kind of overlap Playbook 06 must
   resolve; do not force a premature single-Subdomain assignment here.

## Deliverables

- Candidate Aggregate catalog per Subdomain: Aggregate Root, member
  Entities/Value Objects, consistency rationale, attached Domain Events.
- A cross-Subdomain overlap list for Playbook 06.

## Produced Artifacts

- `docs/discovery/artifacts/05-candidate-aggregates.md`
- `docs/discovery/reports/05-domain-modeling-report.md` (overlap list,
  Entity/Value-Object classification notes, flagged sensitive-data
  Aggregates for Playbook 07)

## Required Diagrams

- Mermaid `classDiagram` per Subdomain showing candidate Aggregates,
  their Entities/Value Objects, and Aggregate Root, stored under
  `docs/discovery/diagrams/`.

## Review Checklist

- [ ] Every Aggregate has exactly one Aggregate Root.
- [ ] Every Entity classification passes the identity test; every Value
      Object classification passes the attribute-equality test — neither
      assigned by default without applying the test.
- [ ] Every Domain Event is attached to a specific Aggregate.
- [ ] No Aggregate embeds another Aggregate by object reference (only by
      ID), per Constitution Section 6.

## Quality Gates

- **Aggregate Size Gate:** any candidate Aggregate with more than a small,
  clearly-justified cluster of Entities/Value Objects is flagged for
  splitting review before Exit (Constitution Section 6's "keep aggregates
  small" rule).
- **DDD Consistency Review** (`domain-driven-design` Quick Diagnostic):
  applied to the full candidate Aggregate catalog.

## Exit Criteria

- Every Subdomain from Playbook 04 has at least one candidate Aggregate (or
  an explicit note explaining why it needs none, e.g., a purely
  process/coordination Subdomain).
- The cross-Subdomain overlap list is complete and handed to Playbook 06.

## Files To Update

- `.claude/context/glossary.md` — append Entity/Value Object/Aggregate
  names as `Draft` Ubiquitous Language terms.

## ADR Impact

None expected — tactical modeling candidates do not rise to
"significant architectural decision" individually. If a single Aggregate's
consistency requirement implies a platform-wide pattern decision (e.g., "we
need Event Sourcing for this one Aggregate's history"), do not decide it
here — log it for Playbook 09/12 and evaluate against the Evolution
Strategy triggers in Constitution Section 55.

## Common Mistakes

- Designing a large, all-encompassing Aggregate "to keep things simple" —
  directly contradicts Constitution Section 6 and the DDD skill's "Giant
  Aggregates" common mistake.
- Embedding a full object reference to another Aggregate instead of
  referencing by ID, silently coupling two Aggregates' consistency
  boundaries together.
- Deciding Bounded Context boundaries at this phase because "it's obvious
  where this Aggregate belongs" — that decision belongs to Playbook 06,
  even when it looks obvious now (Playbook 06 may reveal a Context Mapping
  reason to place it differently).
- Skipping the Entity/Value Object test and defaulting everything to Entity
  "just in case" — produces an anemic, over-mutable model.

## Self Review

For each Aggregate, ask: "if two different actors modify this
concurrently, does the consistency boundary I drew actually prevent an
invalid state?" If not, the Aggregate boundary is wrong and must be
redrawn before Exit.

## Stop Conditions

- A candidate Aggregate cannot be assigned a single, clear Aggregate Root —
  this signals the underlying Subdomain clustering (Playbook 04) may be
  wrong; return to Playbook 04 rather than forcing an arbitrary root.
- A Domain Event from Playbook 03 cannot be attached to any candidate
  Aggregate — flag as a Hotspot for Playbook 06/07 rather than inventing an
  Aggregate to hold it.
