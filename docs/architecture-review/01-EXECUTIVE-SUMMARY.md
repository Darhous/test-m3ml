# Enterprise Adoption Review Board (EARB) — Executive Summary

**Phase:** Enterprise Adoption Review & Technology Baseline Freeze
**Input:** The completed Global Enterprise Build-vs-Buy & Reuse
Intelligence Program (`docs/reuse/`, 28 Modules, 106 Features, 1,378
Feature-level files, 106 logged decisions)
**Output:** A frozen Technology Baseline — mandatory input for API
Platform Strategy, the Software Architecture Document (SAD), Core
Platform, SDK, and Module development, and future ADRs.
**Scope discipline:** This is a **ratification review**, not a new
Build-vs-Buy assessment. No repository was re-searched. Every finding
below traces to an existing `docs/reuse/` artifact, cited by file.

## What This Board Reviewed

- `MASTER_DECISION_REGISTER.md` — 106 rows, every Final Decision
- `MASTER_REPOSITORY_DATABASE.md` — ~55 distinct repositories/standards
  (adopted, evaluated-and-rejected, and Reference-only)
- `MASTER_LICENSE_MATRIX.md` — every candidate's license and obligation
- `MASTER_DEPENDENCY_MATRIX.md` — Cross-Feature reuse and all 9 detected
  duplicate resolutions
- `MASTER_BUILD_VS_BUY_MATRIX.md`, `MASTER_ENGINE_CATALOG.md`,
  `MASTER_LIBRARY_CATALOG.md`, `MASTER_SDK_CATALOG.md`
- `MASTER_READINESS_REPORT.md`, `MASTER_COMPLETION_REPORT.md`
- ADRs 0001–0012, with particular attention to ADR-0011 (Core Domain)
- `.claude/context/open-questions.md`, all 16 tracked questions

## Headline Result

**All 30 Technology Baseline entries are RATIFIED** (21 Engines, 4
Libraries, 5 Reference Standards — see `02-TECHNOLOGY-BASELINE.md`). No
previously "Approved" decision was reversed. No previously "Rejected"
repository is reinstated. Zero duplicate technologies remain active —
the 9 Detected Duplicates from the reuse program were re-verified as
genuinely resolved (2 reactive, 7 proactive), not merely claimed
resolved.

**One decision is downgraded from "Approved" to "Conditionally
Approved, Reconsider at SAD"**: `Eramba Community` for
`compliance-tracking` (Audit and Compliance) — the reuse program itself
logged this as its lowest-confidence decision, and this Board agrees
that status should carry forward unchanged, not be silently upgraded to
full confidence by omission.

**One decision remains explicitly OPEN, not frozen**:
`home-collection-logistics` (Specimen Operations) — genuinely blocked on
Open Question #6 (Offline Mode requirement). This Board does not close
it; closing it would require a product decision this Board is not
authorized to make.

## Critical Governance Finding

**ADR-0011 ("Core Domain — Patient-to-Result Orchestration") is still
formally `Proposed — Amended`, not `Accepted`.** The reuse program
correctly treated it as authoritative for Core Domain preservation
decisions throughout (rejecting OpenMRS, Bahmni, SENAITE, OpenELIS
Global, openIMIS as wholesale replacements) — this Board finds that
usage appropriate given the No-Guessing Rule (treat the best available
proposal as the working assumption, don't invent a different one) but
flags explicitly: **the Technology Baseline's Core-Domain-preservation
logic inherits ADR-0011's own Proposed status.** If ADR-0011 is later
Superseded or its Core Domain framing narrowed, every REFERENCE+BUILD
decision reasoned from it (7 Modules: Patient Management, Practitioner
and Clinic Management, Scheduling and Encounters, Diagnostic Ordering,
Specimen Operations, Laboratory Execution, Result Verification and
Reporting) should be re-examined, not silently carried forward. See
`10-ADR-REVIEW.md`.

## Numbers at a Glance

| Metric | Count |
|---|---|
| Technology Baseline entries ratified (`02-TECHNOLOGY-BASELINE.md`) | 30 |
| Repositories confirmed APPROVED (Engines + Libraries + Reference Standards) | 30 |
| Repositories confirmed REJECTED (evaluated, not selected) | 26 |
| Engines approved | 21 (19 fully approved, 2 conditionally approved with a standing flagged risk) |
| Libraries approved | 4 |
| SDKs approved | 0 (see `05-SDK-BASELINE.md` — genuinely none met the bar) |
| Controlled Forks approved | 0 (see `06-FORK-BASELINE.md`) |
| License categories requiring `Requires Legal Verification` | 13 repositories, all AGPL-3.0 |
| Remaining Open Questions (platform-level) | 4 tracked (#6, #14/ADR-0011, #15, #16) + 1 reuse-program-internal (Eramba confidence) |
| ADRs reviewed | 12 (0001–0012) |
| ADRs recommended for status change | 0 — all recommendations are "no change," see `10-ADR-REVIEW.md` |
| Risks requiring attention before API Strategy | 6, see `11-RISKS.md` |

## Recommendation

The Technology Baseline is **FROZEN** as of this review (`12-DECISION-
FREEZE.md`). The platform is **conditionally ready** to proceed to API
Platform Strategy and SAD work, subject to the AGPL-3.0 legal review
(`08-AGPL-LEGAL-CHECKLIST.md`) being scheduled as an early, explicit
workstream — not a soft dependency easily dropped once implementation
pressure begins.

Per this phase's own Stop Conditions, this Board does **not** begin API
Strategy or Software Architecture work. See `13-READINESS-FOR-API-
STRATEGY.md` and `14-READINESS-FOR-SAD.md` for the formal go/no-go
findings.
