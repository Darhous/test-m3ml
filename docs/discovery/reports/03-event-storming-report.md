# Phase 03 — Event Storming Report

**Execution mode:** Assumption-Driven Autonomous Run.
**Skills applied:** `domain-driven-design` (Domain Events framework),
`mermaid-diagrams` (timeline/sequence diagrams).

## Executive Summary

Storm-walked all 4 Value Streams from Phase 02, surfacing 26 candidate
Domain Events, their triggering Commands, Actors, and External Systems,
plus 5 candidate Pivotal Events and 10 Hotspots. No Hotspot was resolved by
guessing — every one is either logged as a missing-event gap or an Open
Question.

## Findings

- The board is denser around VS1 (10 events) than VS4 (6 events, and the
  shakiest), reflecting how much more Confirmed/Inferred grounding exists
  for the core lab workflow than for billing.
- 4 candidate events are conspicuously *missing* from the initial
  elicitation (equipment failure, failed home visit, chain-of-custody
  handoff, claim denial) — flagged explicitly rather than silently omitted,
  since Constitution Section 34 (Reliability and Resilience) and Section 24
  (Device Integration) both require failure-mode coverage this board does
  not yet have.
- `ResultVerified` and `ResultReleased` are confirmed as the two strongest
  Pivotal Event candidates — both already anticipated informally by the
  Constitution's own illustrative examples (Sections 12, 21, 23), which
  reinforces (but does not fully confirm) their significance.

## Decisions

None (Event Storming is raw-material gathering, per Playbook 03's own "ADR
Impact" section).

## Open Questions

6 new items added this phase (see `OPEN-QUESTIONS-REGISTER.md` entries
4–9). None promoted to `.claude/context/open-questions.md` yet — these are
Hotspots requiring Phase 07 (Business Rules) resolution attempts first,
consistent with `EXECUTION-GUIDE.md` Section 8 ("a new open question
discovered mid-Discovery is appended... when it remains a genuine open
business question" — these are still candidate Hotspots, not yet confirmed
as un-resolvable business questions, so they stay in the Discovery-local
register for now and will be promoted to the Context Store file at Phase
07 or Phase 11/12 if still unresolved then).

## Risks

4 entries (2 carried from Phase 02, 2 new — see `RISK-REGISTER.md` #3–4).
Risk #4 (result-verification authority unresolved) is flagged
Medium-High — the highest severity so far — because it touches clinical
safety directly.

## Assumptions

4 new assumptions logged (`ASSUMPTION-REGISTER.md` #6–9), including an
explicit "gaps are not fabricated" entry (#9) documenting that missing
events were deliberately left missing rather than invented to fill the
board.

## Missing Information

- Real specimen rejection reason taxonomy.
- Real result-verification authority model.
- Real chain-of-custody requirements for home collection.

## Recommendations

- Treat H1 (result-verification authority) as the highest-priority item
  for real user input before Phase 07, given its clinical-safety weight.
- Do not let Phase 04/05 quietly "complete" the 4 missing-event gaps by
  modeling around them — they should surface again explicitly in Phase 07.

## Review Checklist (per Playbook 03)

- [x] Every event name is past tense, Ubiquitous Language, no CRUD-style
      naming.
- [x] Every event traces to a Phase 02 Value Stream — no orphan events.
- [x] Every Hotspot recorded with enough context for later phases to act
      on without re-running this session.
- [x] Pivotal Events marked as candidates only.

## Quality Gates

- **Naming Gate:** PASS — spot-checked all 26 event names against
  Constitution Section 6/40; no generic technical names found.
- **No-Silent-Resolution Gate:** PASS — all 10 Hotspots logged, none
  resolved by assumption.

## Exit Criteria Confirmation

- [x] Every traced Value Stream has a complete, ordered event chain with
      Actors/External Systems identified.
- [x] Every Hotspot logged in the phase report.
- [x] Candidate Pivotal Events identified and hande to Phase 04/06.

## Files Updated

- `.claude/context/glossary.md` (Discovery Phase 03 section appended, 9
  new Draft terms)
- `docs/discovery/artifacts/ASSUMPTION-REGISTER.md`,
  `OPEN-QUESTIONS-REGISTER.md`, `RISK-REGISTER.md` (updated)

## ADR Impact

None (raw material gathering, pre-decision).
