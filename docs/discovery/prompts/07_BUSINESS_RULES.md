# Playbook 07 — Business Rules

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 6 of 11 domain-content phases
**Depends On:** Playbook 06 (fixed Bounded Contexts and Aggregate ownership)
**Produces For:** Playbook 08 (Integrations Discovery needs to know which
rules apply at external boundaries), Playbook 12 (Final Discovery Book's
per-context rule catalog)

---

## Purpose

Extract detailed business rules, invariants, and workflow/state-transition
logic within each now-fixed Bounded Context and Aggregate, refining
Playbook 05's coarse candidate structure into enforceable rules — directly
feeding Constitution Section 25 (Workflow and State Transition Rules) and
Section 21 (Authorization and Data Scope, for rules that gate sensitive
operations).

## Scope

**In scope:** per-Aggregate invariants (what must always be true),
state-transition rules and legal/illegal transitions for Workflow-bearing
Aggregates, cross-Aggregate business rules expressed as policies (not
direct coupling), identification of which rules are Sensitive Operations
under Constitution Section 21 (requiring elevated controls/audit).

**Out of scope:** integration-specific rules with external systems
(Playbook 08); AI-specific governance rules (Playbook 10 — this phase notes
*that* a rule involves AI assistance, not the AI governance detail); final
authorization Policy implementation detail (SAD-level, later).

## Inputs

- `docs/discovery/artifacts/06-bounded-contexts.md`
- `docs/discovery/artifacts/05-candidate-aggregates.md`
- `docs/discovery/artifacts/03-event-storming-board.md` (Hotspots — many
  resolve here)
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 21 (Authorization and
  Data Scope), Section 23 (Audit), Section 25 (Workflow and State
  Transition Rules)

## Preconditions

- Playbook 06 marked complete; Bounded Contexts and Module Ownership fixed.

## Required Skills

- `domain-driven-design` — invariant/consistency-boundary guidance, applied
  in detail now rather than the coarse pass from Playbook 05.
- `architecture-patterns` — for reasoning about where invariant enforcement
  belongs (inside the Aggregate vs. a domain service) without choosing an
  implementation layering (that remains an SAD decision).

## Required Context Files

`constraints.md` (every business rule is cross-checked against existing
Confirmed constraints, e.g., "no autonomous final AI medical decision").

## Project Bindings (this project)

- Any rule governing a verified medical result or consent change is a
  Sensitive Operation per Constitution Section 21 — this phase must flag
  it explicitly so Playbook 12 can confirm Audit Event coverage
  (Constitution Section 23) is planned.

## Execution Steps

1. For each Aggregate from Playbook 06, enumerate its invariants: rules
   that must hold for the Aggregate to be in a valid state at all times.
2. For each Aggregate with a Workflow (multi-step process with states), draw
   its state machine: valid states, valid transitions, and the rule/actor
   that authorizes each transition (per Constitution Section 25).
3. Resolve outstanding Hotspots from Playbook 03 that are business-rule
   Hotspots (as opposed to structural Hotspots already resolved in Playbook
   06) — each resolution is either a direct answer from the user or remains
   `Open`, never guessed.
4. For each rule/transition, classify whether it is a Sensitive Operation
   under Constitution Section 21 (affects verified medical results,
   consent, or cross-tenant administrative action) — if yes, note that
   Audit Event coverage (Section 23) and elevated authorization
   (step-up/dual-control) will be required later.
5. Identify cross-Aggregate business rules (a rule that depends on state in
   more than one Aggregate) and express them as an explicit Policy or
   Process Manager concept referencing both Aggregates by ID — never as
   direct object coupling (preserves Constitution Section 6's aggregate
   isolation).
6. Cross-check every rule against `constraints.md`; a rule that would
   require violating a Confirmed constraint is a Conflict, escalated per
   `EXECUTION-GUIDE.md`, not silently softened.

## Deliverables

- Per-Aggregate invariant catalog.
- Per-Workflow state machine with authorization mapping.
- Sensitive Operation flag list.
- Cross-Aggregate Policy/Process Manager list.

## Produced Artifacts

- `docs/discovery/artifacts/07-business-rules-catalog.md`
- `docs/discovery/artifacts/07-workflow-state-machines.md`
- `docs/discovery/reports/07-business-rules-report.md` (Hotspots resolved
  vs. still open, Sensitive Operation flags, Conflicts raised)

## Required Diagrams

- Mermaid `stateDiagram-v2` per Workflow-bearing Aggregate.
- Mermaid `flowchart` for each cross-Aggregate Policy/Process Manager,
  showing which Aggregates it reads/coordinates.

## Review Checklist

- [ ] Every Aggregate has at least a "no invariants beyond identity" note
      or an explicit invariant list — none silently skipped.
- [ ] Every Workflow's state machine has no unreachable or dead-end state
      without an explicit business reason.
- [ ] Every Sensitive Operation is flagged, not just the "obviously
      medical" ones (e.g., a consent-revocation rule is Sensitive too).
- [ ] No cross-Aggregate rule directly couples two Aggregates by object
      reference.

## Quality Gates

- **Invariant Completeness Gate:** every Hotspot classified as a business-
  rule Hotspot in Step 3 is either resolved or explicitly still `Open` —
  none silently dropped.
- **Sensitive Operation Gate:** cross-checked against Constitution Section
  21's own definition ("verified medical results, consent, or cross-tenant
  administrative actions") — under-flagging is treated as a defect, not a
  simplification.

## Exit Criteria

- Invariant catalog and state machines complete for every Aggregate/
  Workflow from Playbook 06.
- All business-rule Hotspots from Playbook 03 are either resolved or
  explicitly still `Open` in `open-questions.md`.

## Files To Update

- `.claude/context/open-questions.md` — append any business-rule Hotspot
  that remains unresolved.
- `.claude/context/constraints.md` — if a rule surfaces a new Confirmed
  constraint (explicitly confirmed by the user, not inferred), append it
  with the standard Type/Status fields, history preserved.

## ADR Impact

A cross-Aggregate Policy/Process Manager pattern used repeatedly across
multiple Bounded Contexts may warrant a platform-wide ADR at Playbook 12
(e.g., "Process Managers are the standard pattern for cross-Aggregate
business rules") if the pattern proves structural rather than incidental.

## Common Mistakes

- Writing invariants as implementation code/pseudocode instead of business
  rule statements — this phase is still pre-implementation.
- Missing "boring" Sensitive Operations (e.g., a Branch-transfer rule for a
  patient's record) because attention focused only on obviously clinical
  rules.
- Letting a cross-Aggregate rule quietly become a direct dependency between
  two Bounded Contexts, undoing Playbook 06's boundary work.
- Resolving a genuine open business question by picking "the most likely"
  answer instead of leaving it `Open` — a direct No-Guessing Rule violation.

## Self Review

For every Sensitive Operation flagged, re-confirm it against Constitution
Section 21's definition verbatim — do not rely on intuition about what
"feels sensitive."

## Stop Conditions

- A business rule cannot be stated without contradicting a Confirmed
  constraint (e.g., a rule implying an AI can finalize a diagnosis without
  review) — stop, do not soften the rule to fit; escalate as a Conflict.
- A Workflow's state machine has a state with no valid exit and no
  documented business reason (a modeling defect, not a business reality) —
  stop and clarify with the user rather than inventing a resolution.
