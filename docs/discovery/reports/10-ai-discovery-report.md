# Phase 10 — AI Discovery Report

**Execution mode:** Assumption-Driven Autonomous Run.
**Skills applied:** `domain-driven-design` (AI Gateway ACL boundary),
`stride-analysis-patterns` + `threat-mitigation-mapping` (AI data-flow
threats), `api-design-principles` (Gateway contract shape).

## Executive Summary

Identified 7 AI use cases across 5 Bounded Contexts, all within Constitution
Section 28's Permitted list, each with an explicit Human-in-the-Loop or
Data-Scope-filtering design. Rejected 1 candidate outright (auto-verifying
normal results) as a direct Forbidden-list match. Flagged 1 candidate
(notification summarization) as Permitted-but-Not-Ready given a real
practical risk the literal Forbidden list doesn't cover. Logged 1 candidate
(claim auto-approval) as out of Section 28's scope entirely, deferred to
Phase 12's Risk Governance discussion.

## Findings

- Every high-stakes use case (#1, #3, #4) attaches to an already-existing
  Sensitive Operation gate from Phase 07 (Result Verifier Role, explicit
  Order placement) rather than inventing a new approval mechanism — AI
  Discovery did not need to design new governance machinery, only plug into
  what Phase 07 already established.
- The single rejected candidate (R1) is a realistic, plausible-sounding
  efficiency idea, not a strawman — its rejection is a genuine test of
  whether the Forbidden-list gate does real work, and it passed that test.
- Use Case #8 exposes a real gap in Constitution Section 28 itself: the
  Forbidden list is scoped to *decisions*, not to *unreviewed generated
  content* reaching a patient — worth flagging upward, not just handling
  locally.

## Decisions

None (Discovery-level catalog only).

## Open Questions

`.claude/context/open-questions.md` #11 narrowed with the 7-use-case
catalog; explicitly notes none are yet Accepted.

## Risks

1 new entry (`RISK-REGISTER.md` #13 — Use Case #8's literal-vs-practical
gap).

## Assumptions

2 new entries (`ASSUMPTION-REGISTER.md` #25–26).

## Missing Information

- Whether Use Case #8's design gap should be closed by a Constitution
  clarification (Section 28) or purely by implementation-level review
  process — not decided here, flagged for Phase 12.
- Real-world confirmation that any of the 7 use cases are actually wanted
  by the business (all are Inferred, none confirmed).

## Recommendations

- Phase 12 should explicitly discuss whether Risk #13 (Use Case #8's gap)
  warrants raising as feedback on the Constitution itself, not just as a
  Discovery-level design note — this is exactly the kind of finding
  `EXECUTION-GUIDE.md` Section 10 anticipates escalating rather than
  quietly absorbing.
- Do not let Use Case #7 (out-of-scope claim auto-approval) get
  accidentally folded into the AI Governance catalog later — it is a
  financial-automation question, not a medical-AI one, and mixing the two
  would blur Constitution Section 28's clean scope.

## Review Checklist (per Playbook 10)

- [x] Every use case drawn from the Section 28 permitted list — none
      invented outside it.
- [x] Every use case has an explicit Human-in-the-Loop touchpoint design
      (or, for low-stakes cases, an explicit Data-Scope-filtering design in
      its place).
- [x] Every rejected candidate logged with its specific Forbidden-list
      match, not silently dropped.
- [x] No AI provider, model, or vendor named anywhere in this phase's
      output.

## Quality Gates

- **Forbidden-List Gate:** PASS — every candidate explicitly checked; 1
  rejection recorded with reasoning.
- **Human-in-the-Loop Design Gate:** PASS for 7 accepted use cases; Use
  Case #8 correctly logged as **Not Ready** rather than forced through.

## Exit Criteria Confirmation

- [x] AI use-case catalog complete for every context that surfaced a
      candidate.
- [x] Every accepted use case has a HITL/Data-Scope design.
- [x] Every rejected candidate logged with reasoning.

## Files Updated

- `.claude/context/open-questions.md` (item 11 narrowed)
- `docs/discovery/artifacts/ASSUMPTION-REGISTER.md`, `RISK-REGISTER.md`
  (updated)

## ADR Impact

None expected — individual AI use cases implement the already-Accepted
ADR 0007, not new decisions. Risk #13 could motivate a future Constitution
Amendment (Section 45) if the user agrees it's a real gap — flagged, not
decided, here.
