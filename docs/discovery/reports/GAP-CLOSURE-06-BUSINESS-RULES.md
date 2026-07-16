# Gap Closure Wave 6 — Business Rules and Policy Discovery

**Skills used:** `domain-driven-design` (Policy as explicit domain
concept), `architecture-patterns` (policy-engine evaluation-placement
reasoning, no implementation chosen).

## Executive Summary

Delivered the user's most heavily specified requirement — the Configurable
Result Verification Policy Model (8 context dimensions, 4 policy outputs,
4 non-negotiable properties) — as this Wave's centerpiece, explicitly
built as a *refinement* of the Baseline's existing Result Verifier Role
gate, not a contradiction of it. Added a 26-rule representative catalog
across all 24 requested categories. Surfaced a second Sensitive-Operation-
grade rule (Payroll dual-control, echoing Wave 5's finding) and identified
a candidate "Elevated Audit" tier broader than Constitution Section 21's
literal Sensitive Operations definition.

## Findings

- The Verification Policy Model's "safe limits" boundary (what can and
  cannot be configured away) is itself a governance question the future
  SAD/Constitution must answer — Discovery specifies the shape, correctly
  refuses to specify the limit itself without real input.
- The Elevated-Audit-tier finding is a genuine Constitution coverage
  observation, similar in kind to the Baseline's Use Case #8 finding
  (Phase 10) — logged consistently the same way (Recommended, flagged for
  Wave 12/13, not silently applied).

## Decisions

None (Discovery-level rule shapes, not Accepted decisions).

## Open Questions

2 new items (`open-questions.md` #23–24); #23 marked high priority
(directly extends #19, already the highest-priority item in the project).

## Risks

Payroll dual-control and the undesigned Elevated-Audit-tier both carried
to Wave 12 for formal Risk Register consolidation.

## Assumptions

All 26 catalog rules and the Policy Model's illustrative axis values are
`Inferred`, consolidated at Wave 13.

## Files Updated

- `docs/discovery/artifacts/W6-business-rules-and-policy-catalog.md`
  (created)
- `.claude/context/open-questions.md` (items 23–24 appended)

## Review Checklist

- [x] All 24 requested rule categories covered.
- [x] Result Verification Policy Model explicitly reconciled with the
      Baseline's existing rule (refinement, not contradiction — verified
      against Constitution Section 21/25).
- [x] Every rule has Domain Owner, Trigger→Outcome, Config Scope, Audit
      Requirement, Risk Level, Evidence Status.
- [x] No rule silently assumes a specific policy value that should be
      Open.
