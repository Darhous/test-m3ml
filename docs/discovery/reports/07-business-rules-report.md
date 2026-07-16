# Phase 07 — Business Rules Report

**Execution mode:** Assumption-Driven Autonomous Run.
**Skills applied:** `domain-driven-design` (invariants/consistency),
`architecture-patterns` (invariant-enforcement placement reasoning).

## Executive Summary

Produced a full invariant catalog and 4 state machines (TestOrder,
Specimen, TestResult, Claim), each transition explicitly gated with a
named authorizing actor (Constitution Section 25 compliance). Resolved 6 of
10 Phase 03 Hotspots plus 2 Phase 05 gaps *at the modeling level* (a rule
shape now exists); every underlying *business-level* fact remains Open and
was promoted to `.claude/context/open-questions.md` (items 18–22) rather
than guessed. Flagged 3 Sensitive Operations (`ResultVerified`,
`ResultReleased`, `ResultCorrected`) — all within the Core Subdomain,
consistent with its classification.

## Findings

- The Core Subdomain (Test Processing and Result Verification) concentrates
  100% of this catalog's Sensitive Operations — no Sensitive Operation was
  found in any Supporting/Generic context, which is a strong internal-
  consistency signal for the Phase 04 Core Domain proposal.
- Billing/Claims operations were deliberately **not** classified as
  Sensitive Operations under Constitution Section 21's literal definition —
  flagged as Risk #9 for a second look, not silently decided as final.
- Every proposed new event (`TestProcessingFailed`, `HomeVisitFailed`,
  `ResultCorrected`, `ClaimDenied`) exists to make a state machine
  complete, not to add unrequested scope — each traces to a specific
  Hotspot/gap.

## Decisions

None Accepted (Discovery-level rule *proposals* only, per
`DISCOVERY-FRAMEWORK.md` Section 4 — Phase 12 is the only phase that may
promote to Accepted).

## Open Questions

5 new numbered items added to `.claude/context/open-questions.md` (18–22).
Item 19 (Result Verifier eligibility) is flagged **high priority** given
its direct clinical-safety implication.

## Risks

2 new entries (`RISK-REGISTER.md` #9–10).

## Assumptions

2 new entries (`ASSUMPTION-REGISTER.md` #16–17).

## Missing Information

Five business-level thresholds/policies (order expiry window, verifier
eligibility criteria, rejection-escalation threshold, processing-failure
recovery policy, home-visit retry policy) — all logged, none guessed.

## Recommendations

- Prioritize real user input on Open Question #19 (Result Verifier
  eligibility) above all other Phase 07 gaps — it is the only one with
  direct clinical-safety weight.
- Phase 08 should pick up H5/H6 (chain-of-custody, offline mode) and #21/22
  (failure/retry policies) as they are integration-shaped questions, not
  pure business-rule questions.

## Review Checklist (per Playbook 07)

- [x] Every Aggregate has an invariant list or an explicit "identity-only"
      note (none silently skipped — all 6 modeled Aggregates have
      invariants stated).
- [x] Every Workflow's state machine has no unreachable/dead-end state
      without a reason (all 4 traced; `Failed`/`Denied` branches have
      explicit — if Open — recovery paths).
- [x] Every Sensitive Operation flagged, including non-obvious ones
      (billing was *considered* and explicitly excluded with reasoning,
      not silently skipped).
- [x] No cross-Aggregate rule directly couples two Aggregates by object
      reference (all 3 Policies use ID-reference coordination only).

## Quality Gates

- **Invariant Completeness Gate:** PASS — every Phase 03/05 Hotspot/gap
  classified as business-rule-relevant is either resolved at modeling
  level or explicitly Open (12-row Hotspot Resolution Summary table).
- **Sensitive Operation Gate:** PASS — cross-checked against Constitution
  Section 21's literal definition for every rule, including the ones
  ultimately excluded (Specimen rejection, Billing).

## Exit Criteria Confirmation

- [x] Invariant catalog and state machines complete for every Aggregate/
      Workflow from Phase 06.
- [x] All business-rule Hotspots from Phase 03 either resolved (modeling
      level) or explicitly Open in `open-questions.md`.

## Files Updated

- `.claude/context/open-questions.md` (items 18–22 appended)
- `docs/discovery/artifacts/ASSUMPTION-REGISTER.md`,
  `OPEN-QUESTIONS-REGISTER.md`, `RISK-REGISTER.md` (updated)

## ADR Impact

None directly. The Result Verifier Role gate pattern (if it proves
platform-wide, not just Test-Processing-specific) could warrant a
Constitution-level ADR extension at Phase 12 — flagged, not authored here.
