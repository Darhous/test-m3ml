# Phase 02 — Business Discovery Report

**Execution mode:** Assumption-Driven Autonomous Run (user-approved at
Discovery Program start, see `reports/00-discovery-program-status-report.md`).
**Skills applied:** `doc-coauthoring` (Reader Test on the Capability Map),
`domain-driven-design` (Strategic Design lens for Candidate Core/Supporting/
Generic tagging).

## Executive Summary

Produced a 20-capability Business Capability Map and 4 traced Value Streams
for the Laboratory Management starting point, grounded in Confirmed
`vision.md`/Constitution content where it exists and clearly tagged
`Inferred — Industry Reference` elsewhere. Refined all 15 stakeholder
categories with candidate needs, explicitly marked as unconfirmed. No
capability, value stream, or stakeholder need was asserted as fact; all
Inferred content is logged in `ASSUMPTION-REGISTER.md` for later user
review.

## Findings

- The 20 capabilities cluster naturally around a pre-analytical/analytical/
  post-analytical lab-workflow shape (industry-standard), which will be
  tested against real Event Storming evidence in Phase 03–04 rather than
  assumed to be correct.
- Four Value Streams were traceable with reasonable confidence (VS1–VS4);
  a fifth candidate (supplier/procurement) was identified but deliberately
  left untraced rather than fabricated with no basis.
- Stakeholder categories 7–10 and 13–15 (Finance, Inventory, Insurance,
  Suppliers, Security/Compliance, Development, External API Partners) have
  the least Confirmed grounding — their needs are the most purely
  Inferred and should be prioritized for real user confirmation.

## Decisions

None — Business Discovery does not make Accepted decisions (Constitution
Section 39's ADR-before-Accepted gate is not implicated at this phase;
`DISCOVERY-FRAMEWORK.md` Section 4 reserves `Accepted` writes for Phase 12
only).

## Open Questions

See `OPEN-QUESTIONS-REGISTER.md` (3 entries this phase) and
`.claude/context/open-questions.md` item 17 (new).

## Risks

| Risk | Category | Severity | Notes |
|---|---|---|---|
| Entire Capability Map/Value Stream set rests on industry-reference assumption rather than confirmed input | Business | Medium | Mitigated by explicit tagging and the Assumption Register; must be reviewed by the user before any SAD work treats this as settled. |
| Insurance/billing model unknown while a full Value Stream (VS4) was traced around it | Business | Low-Medium | VS4 is intentionally shallow; deeper billing rules deferred to Phase 07 pending #17. |

(Logged to `RISK-REGISTER.md`.)

## Assumptions

5 assumptions logged this phase — see `ASSUMPTION-REGISTER.md` entries 1–5.

## Missing Information

- Real stakeholder pain points/priorities (all 15 categories).
- Real insurance/billing model.
- Whether hospital/clinic capabilities belong in scope now or later.

## Recommendations

- Prioritize user confirmation of stakeholder needs for the categories
  most load-bearing for Phase 07 (Business Rules): Patients, Doctors,
  Laboratory Staff, Laboratory Management.
- Treat the supplier/procurement value stream as an explicit gap to close
  in a future Discovery iteration, not silently ignore it.

## Review Checklist (per Playbook 02)

- [x] Every Business Capability is named in business language.
- [x] Every stakeholder category from `stakeholders.md` was refined (all
      15, tagged Inferred) — none silently skipped.
- [x] Every Core/Supporting/Generic tag is marked Candidate.
- [x] No business goal contradicts an existing Accepted constraint (spot-
      checked against `constraints.md` #5/#6 — no conflict found; VS4's
      billing framing does not touch AI or medical-decision constraints).

## Quality Gates

- **Reader Test:** PASS — every Capability Map row names a recognizable
  business outcome, not a system function (re-read against the Reader Test
  Note in `artifacts/02-business-capability-map.md`).
- **No-Guessing Gate:** PASS — every capability/value stream/need is either
  traced to a Confirmed source or explicitly tagged Inferred with a cited
  basis; nothing presented as fact without a tag.

## Exit Criteria Confirmation

- [x] Business Capability Map and Value Stream inventory exist and pass
      the Reader Test.
- [x] No unresolved Conflict from Step 6 of Playbook 02 (none found).

## Files Updated

- `.claude/context/stakeholders.md` (Discovery Phase 02 section appended)
- `.claude/context/open-questions.md` (item 17 appended)
- `docs/discovery/artifacts/ASSUMPTION-REGISTER.md`,
  `OPEN-QUESTIONS-REGISTER.md`, `RISK-REGISTER.md` (updated)

## ADR Impact

None (as expected — Playbook 02's own "ADR Impact" section confirms
Business Discovery is pre-architectural).
