# Readiness for Software Architecture Document (SAD)

**Verdict: CONDITIONALLY READY.** This mirrors and formally supersedes
`MASTER_READINESS_REPORT.md`'s own verdict, now backed by an independent
Board ratification rather than the reuse program's self-assessment
alone.

## Readiness Checklist

| Item | Status | Note |
|---|---|---|
| Coverage: every Module/Feature has a Build-vs-Buy decision | ✓ Ready | 106/106, 1 explicitly and honestly blocked (`09-OPEN-QUESTIONS.md` #6) |
| Decision quality: every decision is evidence-based, not guessed | ✓ Ready | Re-verified by this Board across all 106 rows, no shallow/fabricated entries found |
| License landscape fully mapped | ✓ Ready | `07-LICENSE-REVIEW.md` |
| AGPL/legal risk explicitly actionable, not just noted | ✓ Ready | `08-AGPL-LEGAL-CHECKLIST.md` — 7 concrete checklist items |
| Duplicate technologies eliminated | ✓ Ready | 9/9 resolved, re-verified in `03-ENGINE-BASELINE.md` Finding 4 |
| ADR-0011 (Core Domain) status accurately preserved | ✓ Ready | `10-ADR-REVIEW.md` — confirmed Proposed, not silently promoted |
| No architectural conflicts between ratified technologies | ✓ Ready | `11-RISKS.md` Task 13 |
| Upgrade compatibility between major Engines assessed | ✓ Ready, 1 new constraint surfaced | `11-RISKS.md` Task 14 — Frappe Framework must be treated as one upgrade unit across 4 Engines |
| Vendor lock-in assessed | ✓ Ready | `11-RISKS.md` Task 15 — no unacceptable lock-in |
| Exit strategies documented | ✗ Gap | `11-RISKS.md` R-08 — fallback *candidates* are named, but no actual exit *procedure* exists yet; this is explicitly assigned to the SAD itself to produce, not a blocker to starting SAD work |
| Open Questions honestly tracked, not fabricated closed | ✓ Ready | `09-OPEN-QUESTIONS.md` — 6 remain open, all with justification |

## What the SAD Inherits As Fixed Input (Do Not Re-Derive)

- `02-TECHNOLOGY-BASELINE.md` — the technology choice for every Feature
  except `home-collection-logistics`
- The Core-Domain-preservation pattern (REFERENCE+BUILD over FHIR
  resources) across 7 Modules, conditional on ADR-0011 as currently
  framed (`10-ADR-REVIEW.md`)
- The 9 duplicate-avoidance boundary decisions in
  `MASTER_DEPENDENCY_MATRIX.md` (e.g., ERPNext vs. OpenBoxes stock
  ownership, Kill Bill vs. ERPNext revenue-domain separation)

## What the SAD Must Still Produce (Not Pre-Empted by This Baseline)

1. The tenant-partitioning technical decision (Open Question #15) —
   this Baseline provides evidence, not the decision.
2. A pinned FHIR version (R-06).
3. Actual exit-strategy procedures for the 7 Tier-1 Engines (R-08).
4. Resolution or explicit carry-forward of the AGPL legal review outcome
   into the SAD's own dependency documentation.
5. Verification of Arabic/RTL localization support for each ratified
   Engine (ADR-0010 gap noted in `10-ADR-REVIEW.md`), since this was not
   a checked criterion during the original Build-vs-Buy research.
6. A decision on the Eramba Community reconsideration (R-01) — the SAD
   is the appropriate venue for the "absolutely necessary" focused
   re-scan this phase declined to perform.

## Board Recommendation

Software Architecture Document work **may begin**, treating
`02-TECHNOLOGY-BASELINE.md` as frozen input per `12-DECISION-FREEZE.md`,
with the 6 items above tracked as the SAD's own explicit early
deliverables — not gaps this Baseline silently hands off unlabeled.

**This Board does not begin Software Architecture work itself.** Per
this phase's Stop Conditions, this document is the final output of the
Enterprise Adoption Review.
