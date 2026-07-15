# Playbook 01 — Master Orchestrator

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** Orchestrator (runs before Phase 02 and gates every subsequent phase)
**Depends On:** none (this is the entry point)
**Produces For:** every other playbook in this framework (it does not produce
domain content itself — it produces and maintains the execution ledger that
every other phase reads and updates)

---

## Purpose

Sequence, gate, and track the execution of the entire Discovery framework
(Playbooks 02–12) so that Discovery proceeds in a controlled, auditable
order instead of an ad hoc conversation. This playbook does not discover
anything about the business or domain itself — it is the control plane for
the eleven playbooks that do.

## Scope

**In scope:** reading the framework definition (`DISCOVERY-FRAMEWORK.md`),
confirming preconditions, invoking Playbooks 02–12 in dependency order,
checking each phase's Exit Criteria before allowing the next phase to start,
maintaining a single execution ledger, and detecting when a Stop Condition
raised by any child playbook should halt the whole run.

**Out of scope:** any business, domain, event, integration, or architecture
content (that is Playbooks 02–11's job); writing the Software Architecture
Document; writing production code.

## Inputs

- `docs/discovery/DISCOVERY-FRAMEWORK.md` (phase order, dependencies, gates)
- `docs/discovery/EXECUTE-DISCOVERY.md` (the operational run script this
  playbook follows)
- `docs/constitution/PROJECT-CONSTITUTION.md` v2 (governing rules)
- `docs/adr/*.md` (Accepted decisions this framework must not contradict)
- `.claude/context/*.md` (current Draft/Proposed/Accepted/Open state)
- The execution ledger from any prior, incomplete run (for resume)

## Preconditions

- `docs/constitution/PROJECT-CONSTITUTION.md` status line reads `Accepted`.
- `git status` is clean on `main` before starting (per `CLAUDE.md` Section
  16 / Constitution Section 42 Git Workflow) — Discovery does not start on
  top of uncommitted, unrelated work.
- No open Exception (Constitution Section 44) or pending Constitution
  Amendment (Section 45) is unresolved that would change a rule Discovery
  depends on.

## Required Skills

- `doc-coauthoring` — to structure the overall multi-phase conversation and
  keep each phase's output reader-testable.
- No domain/diagram/security skill is invoked directly by this playbook —
  each child playbook names its own required skills; this playbook only
  confirms they were invoked when it checks a phase's Exit Criteria.

## Required Context Files

All of `.claude/context/*.md` (read-only at this level; individual phases
update specific files as documented in their own "Files To Update" section).

## Project Bindings (this project)

- Project: digital healthcare platform, `darhous/test-m3ml`, starting point
  Laboratory Management (`.claude/context/vision.md`).
- Governing Constitution: `docs/constitution/PROJECT-CONSTITUTION.md` v2.
- Accepted ADRs this Discovery must not contradict: `docs/adr/0001`–`0010`.

## Execution Steps

1. Read `DISCOVERY-FRAMEWORK.md` in full; confirm the phase order and
   dependency graph have not changed since this playbook was last run.
2. Check Preconditions above. If any fails, stop and report — do not patch
   around a failed precondition silently.
3. Locate or create the execution ledger at
   `docs/discovery/artifacts/00-master-execution-log.md` (template: phase
   number, phase name, status [not started / in progress / blocked /
   complete], start date, completion date, Exit-Criteria-met Y/N, Stop
   Conditions hit, notes).
4. For each phase 02 → 12, in order:
   a. Confirm the phase's own Preconditions and "Depends On" phases are
      marked complete in the ledger.
   b. Invoke the phase's playbook.
   c. On completion, verify the phase's Exit Criteria against its own
      declared checklist — do not mark a phase complete on the phase's own
      say-so without this cross-check.
   d. Update the ledger.
   e. If the phase raised a Stop Condition, halt the entire run at that
      point (see Stop Conditions below) rather than skipping ahead.
5. After Phase 12 completes, confirm the Final Discovery Book exists and is
   internally consistent (Phase 12's own Exit Criteria already require
   this — this step is a final cross-check, not a re-review).

## Deliverables

- A complete, phase-by-phase execution ledger showing the full run from
  Phase 02 through Phase 12.

## Produced Artifacts

- `docs/discovery/artifacts/00-master-execution-log.md`

## Required Diagrams

- None produced directly by this playbook. (The overall phase-flow diagram
  lives in `DISCOVERY-FRAMEWORK.md` as the framework's own reference
  diagram, not as a per-run artifact.)

## Review Checklist

- [ ] Every phase 02–12 appears in the ledger exactly once per run.
- [ ] No phase is marked complete without its Exit Criteria verified.
- [ ] No phase was started before its declared dependencies completed.
- [ ] Every Stop Condition hit during the run is recorded with its
      resolution (resumed, escalated, or run halted).

## Quality Gates

- **Sequencing Gate:** a phase may not start if any phase it depends on
  (per `DISCOVERY-FRAMEWORK.md`'s dependency table) is not yet `complete`
  in the ledger.
- **Exit-Criteria Gate:** a phase may not be marked `complete` in the
  ledger until its own Exit Criteria checklist is fully satisfied.

## Exit Criteria

- Phases 02–12 are all marked `complete` in the ledger, OR the run is
  deliberately halted with a documented reason and resume point (see
  `EXECUTION-GUIDE.md`, "How to Resume").

## Files To Update

- `docs/discovery/artifacts/00-master-execution-log.md` (created/updated
  continuously through the run).

## ADR Impact

None directly. This playbook aggregates, but does not itself decide, ADR
impact signals raised by child playbooks (see each playbook's own "ADR
Impact" section; Playbook 12 is where any resulting new ADRs are actually
authored).

## Common Mistakes

- Running phases out of declared dependency order "to save time."
- Treating a phase as complete because it produced *some* output, without
  checking its Exit Criteria checklist item by item.
- Silently resolving a Stop Condition raised by a child playbook instead of
  escalating per that playbook's own Stop Conditions section.
- Using this playbook to make an actual domain/business decision "just this
  once" instead of delegating to the correct child playbook.

## Self Review

Before declaring the run complete, re-read the ledger top to bottom and
confirm: (a) it tells a coherent story of what happened and in what order,
(b) every "complete" phase has a corresponding Exit-Criteria confirmation,
(c) no phase's artifacts are referenced by a later phase before that phase
ran.

## Stop Conditions

- A Precondition fails.
- A child playbook raises its own Stop Condition.
- A phase's produced artifact contradicts an Accepted rule in the
  Constitution or an Accepted ADR (escalate per Constitution Section 44,
  Exception Process — do not silently reinterpret the Constitution to fit
  the new finding).
- The execution ledger itself is found to be inconsistent (e.g., a phase
  marked complete whose declared dependency is not complete) — halt and
  reconcile before proceeding.
