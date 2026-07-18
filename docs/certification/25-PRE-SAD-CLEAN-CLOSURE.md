# Pre-SAD Baseline Correction & Clean Closure

**Phase:** Pre-SAD Baseline Correction & Clean Closure — a strictly
limited correction phase, not a redesign phase and not the Software
Architecture Document (SAD) itself. **Authoritative starting baseline:**
commit `d152320` (Architecture Readiness Review / Baseline Freeze v1).
**Date:** 2026-07-18.

**Note on the shared "25" prefix:** this document and
`25-EXECUTIVE-CONCLUSION.md` share a numeric prefix by coincidence of
this repository's per-phase file-numbering convention (each phase
numbers its own outputs starting after the previous phase's last
number). They are two distinct files from two distinct phases; neither
replaces the other's filename. `25-EXECUTIVE-CONCLUSION.md` is preserved
unmodified as the Architecture Readiness Review's own historical
conclusion, now carrying a forward-reference note to this document.

## 1. Scope

This phase corrects four specific, named gaps left after the
Architecture Readiness Review, and performs a repository-wide
consistency sweep for the stale references those gaps produced. It does
**not** reopen any Accepted ADR, does not introduce any new technology,
module, architectural style, or product decision beyond the four named
corrections, and does not write any Software Architecture Document
content. The four corrections:

1. Correct the SAD Input Package's Feature-decision count (remove the
   misleading "1 blocked" framing).
2. Establish one consistent governance statement for Kong Gateway and
   OpenBao.
3. Formally adopt PostgreSQL as the primary relational database (new
   ADR).
4. Establish a governed Disaster Recovery baseline (new ADR), without
   fabricating final numeric targets.

## 2. Corrections Completed

**Correction 1 — Decision-count correction.** `home-collection-
logistics` (Module 13, Specimen Operations) was the platform's one
Feature left `DEFERRED — BLOCKED` at reuse-program close. Open Question
#6 (Offline Mode requirement) was resolved during the Open Questions
Resolution phase (Offline Mode = Required, D-48), which architecturally
unblocked the Feature. This phase corrected every document that still
described the reuse program's outcome as "105 decided, 1 blocked" to
instead state precisely: **106 Feature decisions processed, 106
architecturally resolved, 0 architectural blockers.** The Feature's
Build-vs-Buy *classification* (which local-first sync library/engine to
use) is distinguished explicitly as a separate, implementation-level
micro-assessment, not an architectural open question — this is a
distinction, not a demotion; the underlying architectural decision
(Offline Mode is Required) is unchanged.

**Correction 2 — Kong/OpenBao governance clarification.** Every
reference to Kong Gateway and OpenBao across the Architecture Baseline
Freeze, Decision Register, Technology Baseline, API Platform documents,
Open Questions Resolution, SAD Input Package, Project Memory, and
Repository Context was reviewed and made consistent with **one
canonical governance statement**, authored once in
`22-ARCHITECTURE-BASELINE-FREEZE.md` and referenced (not duplicated or
paraphrased) everywhere else. See Section 5 below for the statement
itself. Kong Gateway and OpenBao were also added to the Technology
Baseline as full ratified Engine entries (E22, E23) — they were
previously only recommendations in `docs/api-platform/`, not Baseline
entries.

**Correction 3 — PostgreSQL formally adopted.** `docs/adr/0013-
postgresql-as-primary-relational-database.md` created, Status:
Accepted. See Section 3.

**Correction 4 — Disaster Recovery baseline established.**
`docs/adr/0014-disaster-recovery-and-business-continuity-baseline.md`
created, Status: Accepted. See Section 4.

## 3. ADR-0013 Summary — PostgreSQL as the Primary Relational Database

**Decision:** PostgreSQL is the primary transactional relational
database engine for the platform's Version 1 architecture. This is the
authoritative default relational engine for transactional Module data
unless a future ADR approves an exception.

**What it does not mean:** not every workload must be stored in
PostgreSQL (analytics warehouses, search engines, object storage,
caches, and event brokers remain permitted specialized stores); not
every Module must share one physical database instance (Schema per
Module, ADR-0003, is unaffected); this is not a hosting-provider or
managed-service decision.

**Rationale:** PostgreSQL was already the de facto implied choice
(Hybrid Tenant Isolation's Row-Level Security mechanism and the
pgvector Library both require PostgreSQL specifically); no other Engine
in the ratified Technology Baseline offers an equivalent combination of
RLS, pgvector, license posture, and organizational familiarity.

**Relationship to other decisions:** directly implements the shared-
tier partitioning mechanism (D-42, PostgreSQL RLS + tenant-ID column),
is the substrate Schema per Module (ADR-0003) assumes, and is the only
supported host for the pgvector Library already in the Technology
Baseline. Analytics and event-persistence stores remain explicitly out
of this ADR's scope.

## 4. ADR-0014 Summary — Disaster Recovery and Business Continuity Baseline

**Decision:** a 4-tier service-criticality classification and a full
set of DR architecture principles (backup, restore verification,
geographic/failure-domain, tenant data recovery, encryption/access-
control, dependency recovery responsibility, disaster declaration
governance, DR testing expectations, SaaS/On-Premise/Hybrid mode
relationship) are Accepted.

**What is explicitly NOT Accepted:** any final numeric RPO, RTO,
availability, retention, or regional-topology value. Every numeric cell
in the Recovery Classes table is labeled `*[to be set]*` with an
honest Status: Proposed Target / Pending Business Approval / Pending
Regulatory Validation / Pending Workload Evidence. No number was
invented to fill this gap — per the No-Guessing Rule, a governed
framework with tracked numeric dependencies is delivered instead of a
fabricated commitment.

**Service Criticality Tiers:** Tier 1 (Life/Safety/Clinical — Result
Verification and Reporting, Diagnostic Ordering, Specimen Operations,
Patient Management), Tier 2 (Core Operational — Scheduling and
Encounters, Laboratory Execution, Billing, Insurance and Corporate
Contracts, Identity and Access), Tier 3 (Business Support — Workforce
Management, Payroll, Procurement, Supplier Management, Accounting, CRM
and Support), Tier 4 (Non-Critical Analytics/Auxiliary).

**Effect on SAD readiness:** closes the sole "Missing Inputs" finding
`23-SAD-READINESS-MATRIX.md` identified at the Architecture Readiness
Review. The SAD now inherits a governed classification framework, not a
blank section — final numeric approval remains a tracked, structured,
non-blocking dependency.

## 5. Kong and OpenBao Governance Clarification

**One canonical statement** (authored in full in
`22-ARCHITECTURE-BASELINE-FREEZE.md`, referenced — not restated — by
every other document):

1. The architectural need for an API Gateway and centralized Secrets
   Management is architecturally frozen.
2. Kong Gateway is the approved Version 1 API Gateway product
   selection.
3. OpenBao is the approved Version 1 Secrets Management product
   selection.
4. Neither product may be architecturally re-evaluated during SAD
   authoring — the SAD treats both as fixed input.
5. Both remain subject only to implementation due diligence:
   deployment fit, security hardening, operational compatibility,
   licensing re-verification, and exit-strategy validation.
6. A failed implementation due-diligence gate triggers formal
   governance (an ADR amendment or replacement through Constitution
   Section 45) — it must never silently change the product.

## 6. Decision-Count Correction (Detail)

| Before this phase | After this phase |
|---|---|
| "105 decided, 1 explicitly blocked" (106 Features) | "106 architecturally resolved, 0 architectural blockers" (105 with a Final Decision + 1 unblocked with classification pending a scoped implementation-level micro-assessment) |
| 12 ADRs (10 Accepted, 2 Proposed) | 14 ADRs (14 Accepted, 0 Proposed) |
| Technology Baseline: 21 Engines / 30 entries | Technology Baseline: 24 Engines / 33 entries |
| SAD Readiness Matrix: 19 Ready / 5 Partially Ready / 1 Missing Inputs | SAD Readiness Matrix: 21 Ready / 4 Partially Ready / 0 Missing Inputs |
| Decision Register: 39 decisions | Decision Register: 43 decisions |

## 7. Files Modified

**Created:**
- `docs/adr/0013-postgresql-as-primary-relational-database.md`
- `docs/adr/0014-disaster-recovery-and-business-continuity-baseline.md`
- `docs/certification/25-PRE-SAD-CLEAN-CLOSURE.md` (this document)

**Modified:**
- `docs/reuse/MASTER_BUILD_VS_BUY_MATRIX.md`
- `docs/reuse/MASTER_COMPLETION_REPORT.md`
- `docs/reuse/MASTER_FEATURE_CATALOG.md`
- `docs/reuse/MASTER_EXECUTIVE_SUMMARY.md`
- `docs/api-platform/10-API-GATEWAY.md`
- `docs/api-platform/12-SECRETS-AND-KEYS.md`
- `docs/api-platform/31-ENTERPRISE-PRODUCT-DECISIONS.md`
- `.claude/context/open-questions.md`
- `.claude/context/decisions.md`
- `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`
- `docs/architecture-review/12-DECISION-FREEZE.md`
- `docs/architecture-review/01-EXECUTIVE-SUMMARY.md`
- `docs/architecture-review/09-OPEN-QUESTIONS.md`
- `docs/certification/06-API-CERTIFICATION.md`
- `docs/certification/10-DECISION-REGISTER.md`
- `docs/certification/11-RISK-REGISTER.md`
- `docs/certification/13-PROJECT-MEMORY.md`
- `docs/certification/14-PROJECT-INDEX.md`
- `docs/certification/15-SAD-INPUT-PACKAGE.md`
- `docs/certification/22-ARCHITECTURE-BASELINE-FREEZE.md` (rewritten as Freeze v2)
- `docs/certification/23-SAD-READINESS-MATRIX.md`
- `docs/certification/25-EXECUTIVE-CONCLUSION.md` (supersession note added, historical content preserved)

No file outside `docs/`, `.claude/context/`, and this closure document
was touched. No file in `docs/constitution/`, `docs/discovery/`, or the
0001-0012 ADR files was modified in substance (only cross-reference
indices such as `decisions.md`'s ADR Index table were updated).

## 8. Consistency Search Results

A repository-wide search was run for every term this phase's mandate
named: `"105 decided"`, `"1 blocked"`, Home Collection blocked status,
Kong/OpenBao as merely directional, PostgreSQL implied-not-formal,
Disaster Recovery marked entirely missing, `"12 ADRs"`, ADR counts in
reports/summaries, Technology Baseline entry counts, Architecture
Baseline Freeze counts, readiness scores and matrices, and "next
authorized phase" wording.

**Findings and disposition:**
- All **living/current-state documents** (Decision Register, Project
  Memory, Project Index, SAD Input Package, SAD Readiness Matrix,
  Architecture Baseline Freeze, Technology Baseline, `decisions.md`,
  `open-questions.md`) were corrected in place to the current, accurate
  counts.
- One genuine drift was found and fixed: `11-RISK-REGISTER.md`'s R-14
  row still read "Blocked on Open Question #6... Status: Open" with no
  qualification — corrected to reflect 0 architectural blockers, with
  the residual (Build-vs-Buy micro-assessment) correctly retained as a
  smaller, non-architectural Open item rather than closed outright.
- **Historical audit-trail documents** (`04-ADR-CERTIFICATION.md`,
  `16-EXECUTIVE-DOSSIER.md`, `17-READINESS-SCORES.md`,
  `18-CERTIFICATION-REPORT.md`, `01-FULL-ENTERPRISE-AUDIT.md`,
  `03-ENGINE-BASELINE.md`, `08-LICENSING-CERTIFICATION.md`,
  `docs/api-platform/15-ADR-REVIEW.md`) were **not rewritten** — per
  this phase's own instruction and the convention `15-SAD-INPUT-
  PACKAGE.md` already established, these documents accurately describe
  the ADR/Baseline counts as of their own authoring date and are
  preserved as the historical record. `16-EXECUTIVE-DOSSIER.md` and
  `17-READINESS-SCORES.md` already carried forward-reference notes from
  the Architecture Readiness Review phase; no further change was
  needed. `04-ADR-CERTIFICATION.md`, `18-CERTIFICATION-REPORT.md`,
  `01-FULL-ENTERPRISE-AUDIT.md`, `03-ENGINE-BASELINE.md`, and
  `08-LICENSING-CERTIFICATION.md` are covered by `15-SAD-INPUT-
  PACKAGE.md`'s and `14-PROJECT-INDEX.md`'s existing "historical record,
  not retroactively rewritten" statements.
- Three additional historical documents were given supplementary
  forward-reference notes (without altering their original findings),
  because their headline numbers are prominent enough to plausibly
  mislead a reader about current state: `25-EXECUTIVE-CONCLUSION.md`
  (ARR's own final verdict document), `docs/architecture-review/
  01-EXECUTIVE-SUMMARY.md` (EARB's own headline result), and
  `docs/architecture-review/12-DECISION-FREEZE.md` (the original
  Technology Baseline freeze document whose own Amendment Process this
  phase invoked).
- `docs/certification/06-API-CERTIFICATION.md`'s independent Gateway/
  Secrets re-verification table (accurate "Open" finding at Certification
  Audit time) received a one-line update note.
- `docs/architecture-review/09-OPEN-QUESTIONS.md`'s Open Question #6
  entry (EARB's own "REMAINS OPEN" finding, correctly left open at EARB
  time per the No-Guessing Rule) received a resolution pointer.
- No document was found presenting Home Collection Offline Mode as an
  active architectural blocker after this sweep.
- No document was found presenting Kong or OpenBao as merely directional
  or optional after this sweep (`docs/api-platform/10`, `12`, and `31`
  already carry "Superseded, 2026-07-18" paragraphs from Correction 2).
- `"next authorized phase"` appears once, in `19-CERTIFICATION-CLOSURE-
  REPORT.md`, correctly stating the SAD is the next authorized phase —
  this remains accurate today (no phase since has been the SAD itself)
  and required no change.

## 9. Remaining External Dependencies (13, none architectural — unchanged by this phase)

| Type | Items |
|---|---|
| Legal Dependency | AGPL-3.0 review (5 Engines, R-04), unconfirmed licenses (Novu/Documenso, R-07), general local legal requirements, Egypt cross-border transfer rules |
| Regulatory Dependency | Result Verifier eligibility values, Egypt regulatory consolidated (R-13) |
| Country Localization | Language/currency exhaustive list, Egypt Payroll statutory rules, National ID validation rules |
| Operational Assumption | Expected usage volume, legacy migration N/A |

Plus, newly tracked by ADR-0014: final numeric RPO/RTO/availability/
retention values, explicitly Pending Business/Regulatory/Workload
Approval — a structured, non-blocking dependency, not an unresolved
architectural question.

## 10. Remaining Non-Blocking Risks

15 tracked in `11-RISK-REGISTER.md`, unchanged in count by this phase.
Highest severity: R-02 (Mirth Connect frozen-release), R-04 (AGPL-3.0
legal exposure). R-14 (Home Collection) reduced in substance this phase
— its architectural blocker is resolved; it remains open only as a
Low-Medium, non-architectural, implementation-level tracking item (the
Build-vs-Buy micro-assessment). No risk was newly discovered by this
phase.

## 11. Final SAD Readiness Conclusion

All four required corrections are complete. The consistency sweep found
one genuine drift (`11-RISK-REGISTER.md` R-14) and fixed it; all other
findings were either already-current living documents or correctly-
preserved historical records, several of which received supplementary
forward-reference notes for clarity. No Accepted ADR was reopened. No
new technology, module, architectural style, or product decision was
introduced beyond PostgreSQL (ADR-0013) and the Disaster Recovery
framework (ADR-0014), both explicitly required by this phase's mandate.
No SAD content was drafted.

# CLEAN BASELINE — READY FOR SOFTWARE ARCHITECTURE DOCUMENT
