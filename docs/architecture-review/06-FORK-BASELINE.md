# Fork Baseline — Detailed Validation

## Finding: Zero Controlled Forks Ratified

No Feature in `MASTER_DECISION_REGISTER.md`'s 106 rows carries a
CONTROLLED FORK decision. This Board re-verifies that finding by
scanning all 106 rows for fork-shaped language ("fork," "patched
build," "maintained branch") — none appears as an actual Final
Decision. The taxonomy was available throughout the reuse program
(explicitly listed in its own mission scope) and simply was never the
best-fit answer for any Feature.

## Fork-Adjacent Candidates Considered and Their Actual Classification

Several candidates were named using the word "fork" in the reuse
program's research but were **evaluated as independent projects**, not
adopted as Controlled Forks of the platform's own making:

| Candidate | Nature | Where It Appeared | Classification |
|---|---|---|---|
| Cal.diy | A pre-existing, independently-maintained MIT-licensed community fork of Cal.com | Scheduling and Encounters, `appointment-scheduling-engine` | **Evaluated, not selected** — logged as a credible fallback to Cal.com, not adopted. The platform would not be *creating* a fork; Cal.diy already exists as one, maintained by others. |

No other Feature considered maintaining a platform-owned patched branch
of any upstream Engine. Every ENGINE + ADAPTER decision in the Baseline
uses the upstream project unmodified, integrated via its public API/
plugin surface (Anti-Corruption Layer pattern, per `MASTER_ENGINE_
CATALOG.md`'s "Adapter Boundary" column) — the architecturally
correct reason a Controlled Fork was never needed: every adopted Engine
exposed a sufficient extension point without requiring platform-side
source modification.

## Why This Is a Positive Finding, Not a Gap

A Controlled Fork is the highest-maintenance-burden reuse category (the
platform inherits the obligation to track upstream *and* maintain its
own patch set indefinitely). Zero forks means zero such obligations
exist in the current Baseline — every Engine's adapter boundary was
judged sufficient without source-level modification. This Board
confirms this is architecturally sound, not an under-explored category:
the reuse program's own `03-candidate-repositories.md` files across all
28 Modules never surfaced a case where an Engine's near-fit required
patching rather than configuration/plugin extension.

## Board Findings

- **0 Controlled Forks ratified — confirmed absence.**
- **No action required.** If a future Engine (post-SAD) is found to need
  platform-side patching to meet a requirement its plugin surface can't
  reach, that would be a new CONTROLLED FORK decision requiring its own
  ADR and EARB review cycle — this Baseline does not pre-authorize one.
