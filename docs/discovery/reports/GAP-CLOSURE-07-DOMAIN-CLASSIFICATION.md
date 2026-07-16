# Gap Closure Wave 7 — Domain Discovery and Classification Re-evaluation

**Skills used:** `domain-driven-design` (Strategic Design/Distillation
re-applied enterprise-wide; the Core/Generic distinction specifically
used to reason out "Platform Tenant Operations" as Platform, not Core),
`doc-coauthoring` (Decision Matrix structured for a real user decision,
not a foregone conclusion).

## Executive Summary

Re-classified all discovered domains (Baseline + Waves 3/5) across Core/
Supporting/Generic/Platform. Built a 6-alternative Decision Matrix for the
Core Domain question, explicitly not assuming Test Processing/Laboratory
Execution is final. **Recommends** (not decides) revising ADR 0011 toward
"Patient-to-Result Orchestration" — a reframing that keeps the same
evidence base but better explains the platform's full scope, per Wave 1's
Confirmed Vision.

## Findings

- "Platform Tenant Operations" was reasoned out as Platform-classification,
  not Core — a direct, correct application of DDD's Core-vs-Generic test
  (differentiating value vs. necessary infrastructure), not a dismissal.
- "Clinical Diagnostic Network" has essentially no evidentiary support —
  the weakest alternative, flagged as requiring a business-model
  confirmation the user never gave.
- The evidence-distribution imbalance (Wave 3's finding: Clinical/Lab
  heavily Evidenced, Finance/Workforce/Supply Chain still Inferred)
  directly disqualifies "Healthcare Operations Orchestration" from
  adoption *now*, even though it best matches the Confirmed Vision — a
  disciplined application of the No-Guessing Rule to a strategic
  classification decision, not just a data-fact decision.

## Decisions

None Accepted — this Wave produces a `Recommended` reframing, formally
dispositioned (Retain/Amend/Supersede/Reject) at Wave 14, consistent with
the user's explicit ADR Rules for this program.

## Open Questions

`open-questions.md` #14 annotated with the Wave 7 re-evaluation and
recommendation.

## Risks

Choosing the wrong Core Domain framing has real cost (misdirected deep-
modeling investment) — already captured in the Decision Matrix's "Risk if
Wrong" column rather than duplicated in the Risk Register.

## Assumptions

The entire Decision Matrix rests on Inferred evidence; explicitly flagged
in the matrix itself (Evidence Strength column) rather than asserted as
settled analysis.

## Files Updated

- `docs/discovery/artifacts/W7-domain-classification-reevaluation.md`
  (created)
- `.claude/context/open-questions.md` (item 14 annotated further)

## Review Checklist

- [x] Test Processing/Laboratory Execution explicitly NOT assumed final —
      5 real alternatives compared against it.
- [x] Each alternative scored on Evidence/Differentiation/Buy-vs-Build/
      Scope-Coherence/Risk.
- [x] Buy-vs-build-vs-commodity question directly answered.
- [x] Recommendation clearly labeled Recommended, not Confirmed or
      Accepted.
