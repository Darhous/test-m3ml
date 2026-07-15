# EXECUTE-DISCOVERY — Operational Run Script

**This file does not execute Discovery.** It is the compact, literal
operational reference that a future single prompt ("run Discovery") will
follow to invoke Playbooks 02–12 in sequence. It is derived from, and must
stay consistent with, `DISCOVERY-FRAMEWORK.md` (the *what/why*) and
`EXECUTION-GUIDE.md` (the *how*, session-to-session). If this file and
either of those two ever disagree, `DISCOVERY-FRAMEWORK.md` and
`EXECUTION-GUIDE.md` are authoritative — update this file to match, not the
reverse.

**Preconditions to even begin using this file:**
- `docs/constitution/PROJECT-CONSTITUTION.md` status is `Accepted` (currently
  v2).
- `git status` is clean on `main`.
- The user has explicitly instructed a Discovery run to begin (this file is
  a reference for that future instruction — it does not authorize itself to
  run).

---

## Step 0 — Initialize

1. Read, in order: `docs/constitution/PROJECT-CONSTITUTION.md`,
   `docs/adr/0001`–`0010`, `CLAUDE.md`, all of `.claude/context/*.md`,
   `docs/discovery/DISCOVERY-FRAMEWORK.md`, `docs/discovery/
   EXECUTION-GUIDE.md`.
2. Check for an existing `docs/discovery/artifacts/00-master-execution-log.md`.
   If present, this is a **resume** — follow `EXECUTION-GUIDE.md` Section 7
   and jump to the first incomplete phase below. If absent, this is a
   **fresh start** — create it from Playbook 01's template and begin at
   Phase 02.
3. Confirm `git status` is clean. If not, stop and surface it — do not
   begin Discovery on top of unrelated uncommitted work.

## Step 1 — Run Playbook 01 (Master Orchestrator)

Invoke `docs/discovery/prompts/01_MASTER.md`. Confirm its own Preconditions.
This establishes/validates the execution ledger that every subsequent step
in this script reads and writes.

## Step 2 — Run Phases 02 → 12 in Order

For each phase `N` in `[02, 03, 04, 05, 06, 07, 08, 09, 10, 11, 12]`:

1. **Gate check** — confirm every phase `N` depends on
   (`DISCOVERY-FRAMEWORK.md` Section 3 table) is `complete` in the ledger,
   verified against that dependency's actual Exit Criteria, not merely its
   presence.
2. **Invoke** `docs/discovery/prompts/<NN>_<NAME>.md` in full.
3. **Produce** every artifact/report/diagram that playbook's own
   Deliverables/Produced Artifacts/Required Diagrams sections name — no
   more, no less (do not let a phase's output creep into a later phase's
   territory, per `DISCOVERY-FRAMEWORK.md` Section 1's Single
   Responsibility justification).
4. **Run skills** exactly as that playbook's own "Required Skills" section
   names them — see the Skill Invocation Map below for the consolidated
   view.
5. **Check** that playbook's own Review Checklist and Quality Gates.
6. **Detect contradictions** as they arise during the phase (do not defer
   all contradiction-catching to Phase 11 — Phase 11 catches *cross-phase*
   issues; an in-phase contradiction against an Accepted Constitution
   rule/ADR must be caught immediately, per that phase's own Stop
   Conditions).
7. **On a Stop Condition or Conflict:** halt this script entirely at the
   current phase. Follow `EXECUTION-GUIDE.md` Section 10 (Conflicts) or the
   specific playbook's Stop Conditions section. Do not proceed to phase
   `N+1`. Resume only after the conflict/stop condition is explicitly
   resolved by the user.
8. **On successful Exit Criteria:** update the files in that playbook's
   "Files To Update" section (append-only, status-tagged, never a silent
   `Accepted` write except in Phase 12 — see Step 3 below).
9. **Update the ledger:** mark phase `N` `complete`, record completion
   date and one-line summary.
10. **Commit and push** (see "Git Checkpoints," below) before moving to
    phase `N+1`.

## Step 3 — Special Handling for Phase 11 (Validation)

Phase 11 does not run like the others — it re-reads *all* artifacts from
Phases 02–10 as a single body of work, not just the previous phase's
output. Before invoking it:

- Confirm the ledger shows Phases 02–10 all `complete`.
- Gather the full artifact/report list from `docs/discovery/artifacts/` and
  `docs/discovery/reports/` for Phase 11 to consume.

Its Stop Conditions are stricter than any other phase's: **any** unresolved
contradiction or unmitigated/unowned STRIDE threat halts progress to Phase
12, full stop, regardless of how much of Phases 02–10 "felt" ready.

## Step 4 — Special Handling for Phase 12 (Final Discovery Book)

Only Phase 12 may:
- Write `Accepted` status into a `.claude/context/*.md` file.
- Author a new ADR under `docs/adr/`.

Both actions require that the specific finding being promoted was
explicitly validated (zero contradiction) in Phase 11 — Phase 12 re-checks
this per finding before promoting it; it does not promote everything Phase
11 merely "didn't flag."

After Phase 12's Exit Criteria are met, the overall Discovery run is
complete per `DISCOVERY-FRAMEWORK.md` Section 10's Definition of Complete —
confirm every checklist item there before declaring the run finished.

## Skill Invocation Map (consolidated, for quick reference)

| Skill | Invoked in Phases |
|---|---|
| `doc-coauthoring` | 01, 02, 11, 12 |
| `domain-driven-design` | 02, 04, 05, 06, 08, 09, 10, 11 |
| `architecture-patterns` | 07, 09 |
| `architecture-decision-records` | 12 only |
| `api-design-principles` | 10, 11 |
| `stride-analysis-patterns` | 08, 10, 11 |
| `threat-mitigation-mapping` | 10, 11 |
| `c4-architecture` | 06, 08, 12 |
| `mermaid-diagrams` | 02, 03, 05, 06, 07, 08, 09, 10, 11, 12 |

This table is a navigation aid derived from each playbook's own "Required
Skills" section — if it and a playbook file ever disagree, the playbook
file is authoritative (this table is regenerated from the playbooks, not
the other way around).

## When Reports Are Created (quick reference)

Every phase 02–10 produces its own report at that phase's own completion
(not deferred). Phase 11 produces two cross-phase reports. Phase 12
produces the Discovery Completion Report. Full detail:
`DISCOVERY-FRAMEWORK.md` Section 6.

## When Diagrams Are Created (quick reference)

At the phase that owns the content being visualized — never batched or
deferred to Phase 11/12. Full detail: `DISCOVERY-FRAMEWORK.md` Section 7.

## When Context Is Updated (quick reference)

After every phase, append-only, status-tagged, per that phase's own "Files
To Update" section. Only Phase 12 writes `Accepted`. Full detail:
`DISCOVERY-FRAMEWORK.md` Section 4.

## When ADRs Are Updated (quick reference)

Only Phase 12 authors ADRs, and only for findings Phase 11 validated with
zero contradiction. Full detail: `DISCOVERY-FRAMEWORK.md` Section 5.

## How Contradictions Are Detected

- **In-phase:** each playbook's own Stop Conditions/Quality Gates catch
  contradictions against the Constitution/ADRs visible from within that
  phase's own scope.
- **Cross-phase:** Phase 11's Contradiction Review (its Execution Step 1)
  is the single place the *entire* accumulated Discovery output is diffed
  against Constitution Sections 5–37, all 10 ADRs, and every
  Accepted/Confirmed Context Store item.
- **Resolution path:** always `EXECUTION-GUIDE.md` Section 10 — stop,
  state plainly, escalate to the user, never self-resolve.

## How Quality Review Happens

- **Per-phase:** that phase's own Review Checklist + Quality Gates (every
  playbook has both).
- **Cross-phase:** Phase 11 in full (DDD consistency, full STRIDE +
  mitigation mapping, completeness check, terminology consistency, diagram
  syntax validation, Reader Testing) — see
  `docs/discovery/prompts/11_VALIDATION.md` for the complete method.
- **Final:** Phase 12's Reader Test on the compiled Discovery Book and
  Completion Report.

## How the Final Discovery Book Gets Created

Exactly as `docs/discovery/prompts/12_FINAL_DISCOVERY_BOOK.md` Execution
Steps 1–7 specify: assemble from Validation-passed artifacts only (never
from memory/impression of the phases), author any warranted ADRs, update
Context Store files, produce the Completion Report, Reader Test both before
declaring done. No shortcuts, no partial compilation from an incomplete
Phase 11.

## Git Checkpoints

Applied identically at every phase boundary (`EXECUTION-GUIDE.md` Section 6):

1. `git status` clean check before starting the phase.
2. Phase runs, produces artifacts, updates Context files, updates the
   ledger.
3. `git add` the specific paths touched by that phase (artifacts, reports,
   diagrams, the ledger, and any Context Store files updated — never a
   blanket `git add -A`/`git add .`).
4. `git diff --cached --check` (whitespace/conflict-marker sanity check).
5. One commit per phase, message pattern: `docs: discovery phase NN —
   <phase name>` (e.g., `docs: discovery phase 04 — domain discovery`),
   consistent with this project's existing commit style.
6. `git pull --rebase origin main`, then `git push origin main`. No force
   push, ever. On rejection or conflict: stop, surface it, do not resolve
   by guessing (`CLAUDE.md` Section 16).
7. Only after a successful push does the script proceed to gate-checking
   the next phase.

## Stop Points (consolidated)

This script halts, and does not self-resume, at any of:

- Any individual phase's own Stop Conditions (see that phase's playbook).
- A Conflict per `EXECUTION-GUIDE.md` Section 10.
- A failed `git status` clean-check, or a rejected/conflicting push.
- Phase 11 finding any unresolved contradiction or unmitigated/unowned
  STRIDE threat (blocks Phase 12 unconditionally).
- Phase 12 needing to invent a detail to write an ADR or Context update
  (per Playbook 12's own Stop Conditions) — it stops and reports the gap
  instead.

At every stop, the ledger (`docs/discovery/artifacts/
00-master-execution-log.md`) is left in a state that makes resumption
unambiguous, per `EXECUTION-GUIDE.md` Section 7.
