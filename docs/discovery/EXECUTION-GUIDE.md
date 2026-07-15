# Discovery Execution Guide

**Purpose of this document:** a practical, process-level guide for whoever
(human or AI session) actually runs Discovery — how to start, what happens
after each playbook, when to stop, when to review, when to touch git, how
to resume after an interruption, and how to handle the three things that
derail most Discovery efforts: unanswered questions, unstated assumptions,
and conflicts with existing decisions. `DISCOVERY-FRAMEWORK.md` defines
*what* the phases are and *why*; this document defines *how* to operate
them session-to-session. `EXECUTE-DISCOVERY.md` is the compact, literal
run-script derived from both.

---

## 1. How Discovery Is Run

Discovery runs as a sequence of 12 playbook invocations
(`docs/discovery/prompts/01`–`12`), each a self-contained prompt with its
own Purpose/Scope/Execution Steps/Exit Criteria. A session runs one
playbook at a time, in the dependency order fixed by
`DISCOVERY-FRAMEWORK.md` Section 3, and does not start playbook N+1 until
playbook N is verified `complete` in the execution ledger
(`docs/discovery/artifacts/00-master-execution-log.md`, maintained by
Playbook 01).

Concretely, for each playbook:

1. Read the playbook file in full.
2. Confirm its Preconditions and Required Context Files are actually
   satisfied (do not assume — check).
3. Work through its Execution Steps.
4. Produce its Deliverables/Produced Artifacts/Required Diagrams exactly as
   named.
5. Run its own Review Checklist and Quality Gates before considering it
   done.
6. Confirm its Exit Criteria are met.
7. Update the files named in its "Files To Update" section.
8. Update the execution ledger.

## 2. Execution Order

Fixed: 01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 09 → 10 → 11 → 12, per
`DISCOVERY-FRAMEWORK.md` Section 3's dependency table. 08, 09, and 10 each
depend on 06 and 07 but not on each other — they may be worked in any
relative order among themselves (08 before 09 before 10 is the framework's
default reading order, but 09 or 10 could run first without violating any
dependency, since neither consumes the other's output directly). 11
strictly requires all of 02–10 complete. 12 strictly requires 11 complete.

## 3. What Happens After Each Playbook

After every playbook's Exit Criteria are confirmed met:

1. **Update the execution ledger** (Playbook 01's artifact) — mark the
   phase `complete`, record the completion date and a one-line summary.
2. **Update Context Store files** named in that playbook's "Files To
   Update" section — always append-only, always status-tagged, never a
   silent `Accepted` promotion (that is reserved for Playbook 12 only, per
   `DISCOVERY-FRAMEWORK.md` Section 4).
3. **Commit** (see Section 6, below).
4. **Check whether the next phase's Preconditions are satisfied** before
   starting it — do not chain phases automatically without this check, even
   if the previous phase "felt complete."

## 4. When to Stop

Stop the run (halt before starting the next playbook) whenever:

- A playbook's own **Stop Conditions** section fires (every playbook has
  one — read it before starting that playbook, not after hitting trouble).
- A **Conflict** is found between a Discovery finding and an Accepted
  Constitution rule or ADR (see Section 9, below) — this always stops the
  run at that point; it is never resolved by continuing and "fixing it
  later in Validation." Validation (Playbook 11) catches what earlier
  phases could not see, not what they already saw and ignored.
- A required input from the user (a business fact, a stakeholder answer, a
  genuine decision) is missing and cannot be inferred without violating the
  No-Guessing Rule.
- `git status` is not clean going into a phase that is about to write
  Context Store updates (per `CLAUDE.md` Section 16) — reconcile before
  proceeding.

Stopping is not a failure state — it is the framework working as intended.
A run that stops five times to ask real questions and produces accurate
findings is strictly better than a run that never stops and produces
guessed ones.

## 5. When to Review

- **Per-phase review** happens inside every playbook (its own Review
  Checklist and Quality Gates) — this is not optional and is not deferred.
- **Cross-phase review** happens exactly once, in Playbook 11 (Validation),
  after all of 02–10 are complete — do not attempt an ad hoc cross-phase
  review mid-run; Playbook 11 exists precisely because cross-phase issues
  are invisible until the full picture exists.
- **Final review** happens in Playbook 12 (the Reader Test on the compiled
  Discovery Book and Completion Report).

## 6. When to Commit and When to Push

Following `CLAUDE.md` Section 16 / Constitution Section 42's existing Git
Workflow, applied to Discovery specifically:

- **Commit after each completed playbook**, not mid-playbook and not
  batched across multiple playbooks — one commit per phase keeps the
  history exactly as auditable as the execution ledger itself, and makes it
  possible to bisect "which phase introduced this artifact."
- **Push after each commit**, per the existing Git Workflow rule (`git pull
  --rebase origin main` before starting work, clear commit, `git push
  origin main` after each completed stage) — do not accumulate multiple
  phases' commits locally before pushing.
- **Never force push.** If a push is rejected or conflicts, stop and
  surface the conflict — do not resolve it by guessing which side is
  correct (same rule as every other git operation in this project).
- The **Master Orchestrator's ledger update** (Section 3, Step 1 above) is
  part of the same commit as the phase's own artifacts — the ledger and the
  work it describes must never drift apart in git history.

## 7. How to Resume If Interrupted

1. Read `docs/discovery/artifacts/00-master-execution-log.md` — it is the
   single source of truth for "what phase are we on."
2. Find the last phase marked `complete`. If the next phase is marked
   `in progress` or `blocked`, read that phase's own Stop Conditions
   section and its report (if one exists) for the reason it did not
   finish.
3. Re-confirm that phase's Preconditions still hold (context may have
   changed since the interruption — e.g., a Constitution amendment).
4. Resume from the first incomplete Execution Step of that phase — do not
   restart the phase from scratch unless its partial output is actually
   inconsistent (in which case, say so and restart deliberately, not
   silently).
5. If the ledger itself is missing or corrupted, treat this as a Playbook
   01 Stop Condition ("execution ledger is found to be inconsistent") and
   reconcile it against whatever `docs/discovery/artifacts/` and `reports/`
   files actually exist before resuming any content phase.

## 8. How to Handle Open Questions

Every playbook that touches `.claude/context/open-questions.md` follows the
same discipline, inherited directly from that file's own update rule:

- A question is **narrowed** (evidence recorded, still `Open`) when
  Discovery finds relevant information but not a definitive answer — this
  is the common case and is not a failure.
- A question is **answered** only when the user gives an explicit,
  definitive answer during a Discovery session — Discovery playbooks elicit
  this; they do not manufacture it from inference.
- A **new** open question discovered mid-Discovery (e.g., a Hotspot from
  Event Storming that turns out to be a genuine open business question) is
  **appended** to `open-questions.md` with the next sequential number —
  existing items are never renumbered or deleted.
- An answered question is moved to the appropriate file (`constraints.md`,
  `decisions.md`, `vision.md`, per that question's nature) following
  `open-questions.md`'s own "طريقة التحديث" (update method) section, with a
  status note left behind pointing to where the answer now lives.

## 9. How to Handle Assumptions

**The framework's default posture is: no assumptions.** Every playbook's
own Quality Gates include a "No-Guessing Gate" or equivalent, and every
playbook's Common Mistakes section calls out its own specific
assumption-risks. Practically:

- If a fact is needed and not available, **ask the user** — do not infer it
  from "typical healthcare platforms usually..." reasoning, even when that
  reasoning is plausible.
- If a fact is genuinely unknowable at Discovery time (e.g., real
  production scale before launch), **say so explicitly** in the relevant
  artifact/report rather than picking a plausible placeholder number (this
  mirrors exactly how Constitution Section 51's Non-Functional Budgets
  handle the same situation).
- The only exception: a playbook's own Execution Steps may direct a
  **first-pass, explicitly-labeled candidate** (e.g., Playbook 04's
  Core/Supporting/Generic classification, Playbook 05's candidate
  Aggregates) — these are not "assumptions" in the forbidden sense, because
  they are structurally revisited by a later phase (06 formalizes what 04/05
  proposed) and are never written to a Context Store file as `Accepted`.

## 10. How to Handle Conflicts

A **Conflict**, in this framework's vocabulary, is specifically: a
Discovery finding that cannot be true simultaneously with an Accepted
Constitution rule, an Accepted ADR, or a Confirmed constraint in
`.claude/context/constraints.md`. This is distinct from an **Open
Question** (missing information) and distinct from a **Hotspot** (business
ambiguity to be resolved with more discussion) — a Conflict is a genuine
collision between what Discovery is finding and what the project has
already, formally decided.

When a Conflict is found:

1. **Stop** the current playbook at the point the Conflict was found — do
   not continue past it "to finish the phase" first.
2. **State the Conflict plainly**: which finding, which specific
   Constitution Section/ADR/constraint it collides with, and why it is not
   merely an interpretation difference.
3. **Escalate to the user**, per Constitution Section 44 (Exception
   Process) — the user decides one of: (a) the finding is wrong and should
   be revised, (b) this is a genuine Exception requiring documentation
   under Section 44, or (c) this reveals the existing rule needs a
   Constitution Amendment (Section 45) or a superseding ADR. **Discovery
   itself never makes this decision** — every playbook that can raise a
   Conflict says so explicitly in its own Stop Conditions section, and none
   of them are authorized to resolve one unilaterally.
4. **Record the resolution** in the relevant phase report, and only then
   resume.

This is the single most important discipline in the entire framework: it
is what stops Discovery from quietly drifting the project away from its
own Constitution one small rationalization at a time.
