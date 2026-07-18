# Consolidated Open Questions Register

**Superseded 2026-07-18 by the Open Questions Resolution phase — see
`20-OPEN-QUESTIONS-RESOLUTION.md` for the authoritative resolution of
all 31 questions.** This document's original priority/timing
classification (below) is preserved as historical record and remains
accurate as *analysis*; it is no longer accurate as a statement that
"no question is closed" — 18 of the 31 are now resolved (Accepted
Decision/Configuration), 13 remain tracked as genuine Legal/Regulatory/
Country dependencies. The **Resolution Status** table immediately below
is the current state; everything after it is the original, still-valid
prioritization analysis.

## Resolution Status (2026-07-18)

| # | Status | Resolution |
|---|---|---|
| 1 | Resolved | Accepted Decision |
| 2 | Dependency | Legal Dependency (architecture posture decided) |
| 3 | Resolved | Accepted Decision (ADR-0009, confirmed closure) |
| 4 | Resolved | Operational Assumption |
| 5 | Resolved | Accepted Decision + Implementation Decision |
| 6 | Resolved | Accepted with Constraints (Offline Mode required for Home Collection) |
| 7, 8 | Resolved | Accepted Decision (ADR-0005, confirmed closure) |
| 9 | Resolved | Product Configuration |
| 10 | Resolved | Accepted Decision + Country Localization |
| 11 | Resolved | Accepted Decision (mechanism) + Product Configuration (use cases) |
| 12 | Resolved | Accepted Decision (mechanism) + Country Localization (list) |
| 13 | Resolved | Operational Assumption (N/A for v1) |
| 14 | **Resolved** | **Accepted Decision — ADR-0011 Accepted, Core Domain = Patient-to-Result Orchestration** |
| 15 | Resolved | Product Configuration — PostgreSQL RLS + tenant-ID column |
| 16 | Resolved | Accepted Decision (qualitative trigger) |
| 17 | Resolved | Accepted Decision — architecture supports all 3 models, Tenant-configurable |
| 18, 20, 22 | Resolved | Implementation Decision (mechanism Accepted, values deferred) |
| 19, 23 | Resolved | Accepted Decision (mechanism) + Regulatory Dependency (values) |
| 21 | Resolved | Accepted Decision — Degraded-Mode recovery workflow |
| 24 | Resolved | Accepted Decision — Elevated Audit tier adopted |
| 25 | Dependency | Legal Dependency (architecture posture decided) |
| 26 | Dependency | Country Localization Dependency (mechanism decided) |
| 27 | Resolved | Accepted Decision (field) + Country Localization (validation rules) |
| 28 | Resolved | Product Configuration — Kong Gateway (Apache-2.0) |
| 29 | Resolved | Product Configuration — OpenBao (MPL-2.0) |
| 30 | Resolved | Accepted Decision — generated-docs Portal for v1 |
| 31 | Resolved | Accepted Decision — Superset, no new tool |

**Remaining tracked Dependencies (13): #2, #6's Egypt-specific detail,
#12's exhaustive list, #19/#23's specific eligibility values, #25, #26,
#27's validation rules, plus R-04 (AGPL) and R-13 (Egypt regulatory,
non-architectural).** All are Legal, Regulatory, or Country Localization
items outside architectural authority — none blocks SAD start.

---

## Original Priority/Timing Analysis (historical, still valid as analysis)

| # | Question | Priority | Resolution Required |
|---|---|---|---|
| 1 | Target countries/markets | Medium | During SAD (Egypt confirmed as first market; broader expansion architecture can be designed generically) |
| 2 | Local legal/regulatory requirements | High | Before SAD finalizes compliance-sensitive sections |
| 3 | Cloud / On-Premise / Hybrid hosting | Low | Already substantially answered — ADR-0009 (SaaS-First, On-Premise/Hybrid-Ready) Accepted; residual detail During SAD |
| 4 | Expected usage volume | **Critical** | Before SAD finalizes any capacity/scaling/SLA/rate-limit numeric target (blocks R-11, D-26) |
| 5 | Device protocol categories | Low | Candidate list exists (HL7 v2, ASTM, Vendor API); confirmed protocols During SAD/Implementation |
| 6 | Offline Mode requirement | **High** | Before SAD finalizes Scheduling/Specimen Operations Module boundaries (blocks R-14, the sole undecided Feature) |
| 7 | Multi-Tenancy strategy (Tenant per DB vs. Shared+ID) | Low | Already substantially answered — ADR-0005 (Hybrid) Accepted; residual detail is Q15 |
| 8 | Data isolation type between Organizations | Low | Covered by ADR-0005; residual detail is Q15 |
| 9 | Hospitals/clinics in v1 or labs-only first | Medium | Before SAD scopes v1 Module activation order |
| 10 | Notification channels required | Low | Candidate list exists; confirmed channels During SAD/Implementation |
| 11 | AI usage boundaries | Low | Substantially answered — Constitution §28 + 7 candidate use cases with HITL bounds; residual detail During Implementation |
| 12 | Languages/currencies to support | Medium | Before SAD finalizes localization-dependent sections (ADR-0010 sets the principle, not the exhaustive list) |
| 13 | Legacy system migration needs | Low | No evidence exists either way; After SAD unless a real legacy system is identified |
| 14 | Core Domain identification | **Critical** | Before SAD finalizes Core-Domain-dependent Module boundaries (blocks R-15, D-11) — requires Constitution §45 Amendment process |
| 15 | Exact shared-tier partitioning technology | **High** | During SAD — this is explicitly named as one of the SAD's own required early deliverables in `docs/architecture-review/14-READINESS-FOR-SAD.md` |
| 16 | Tenant promotion-path trigger | Medium | During SAD |
| 17 | Actual billing/insurance model (Direct/Reimbursement/Capitation) | Medium | Before SAD finalizes Billing/Insurance Module design |
| 18 | Order Expiry duration | Low | Implementation Phase |
| 19 | Result Verifier Role eligibility criteria | **High** | Before SAD — direct clinical-safety impact (Constitution §21) |
| 20 | Repeated-rejection escalation threshold (N) | Low | Implementation Phase |
| 21 | Processing-failure/device-outage recovery policy | Medium | During SAD |
| 22 | Home-collection visit retry policy | Low | Implementation Phase (contingent on Q6) |
| 23 | Result-verification policy axis values | **High** | Before SAD — tied directly to Q19's clinical-safety priority |
| 24 | Second "Elevated Audit" tier needed? | Medium | During SAD |
| 25 | Egypt cross-border data transfer rules (Law 151/2020) | High | Before SAD finalizes data-residency architecture |
| 26 | Egypt labor/social-insurance law impact on Payroll | Medium | Before SAD finalizes Payroll Module, or During SAD if Payroll is not v1-critical |
| 27 | National ID as core Patient field? | Medium | Before SAD finalizes Patient Management data model |
| 28 | API Gateway product selection | **High** | Before SAD finalizes Edge-layer implementation detail; does not block SAD *starting* |
| 29 | Secrets/Vault Engine selection | **High** | Same as #28 |
| 30 | Developer Portal product selection | Medium | During SAD or later — entangled with #28, lower urgency than the Gateway itself |
| 31 | API Analytics dedicated tool need | Low | After SAD — requires real production data to answer at all |

## Classification Summary

Re-verified this closure pass by direct recount of the 31 per-row
Priority values above (not re-derived, only mechanically recounted —
no priority value was changed from the original register).

| Priority | Count | IDs |
|---|---|---|
| Critical | 2 | #4, #14 |
| High | 8 | #2, #6, #15, #19, #23, #25, #28, #29 |
| Medium | 10 | #1, #9, #12, #16, #17, #21, #24, #26, #27, #30 |
| Low | 11 | #3, #5, #7, #8, #10, #11, #13, #18, #20, #22, #31 |

**2 + 8 + 10 + 11 = 31.** Matches the per-row table exactly. (Prior
version of this summary contained an arithmetic error — Medium was
misstated as 12 and Low as 9, with a stray "#2/#25 borderline" note
that did not correspond to any actual reclassification. No question's
Priority value changed; only the summary's own count was corrected to
match the table it summarizes.)

## Resolution-Timing Summary

**Terminology clarification (this closure pass):** the timing bucket
previously labeled "Before SAD" is renamed **"Blocks Finalization of a
Specific SAD Section"** to remove any ambiguity with "blocks SAD from
starting" — no question in this register blocks SAD work from
starting; see `18-CERTIFICATION-REPORT.md`'s "Formal Certification
Conditions vs. Additional SAD Section Finalization Dependencies"
section for the authoritative statement of this distinction. Counts
below are recounted directly from the per-row "Resolution Required"
column (not re-derived; no question's resolution-timing description
was changed).

| Timing | Count | IDs |
|---|---|---|
| Blocks finalization of a specific SAD section | 13 | #2, #4, #6, #9, #12, #14, #17, #19, #23, #25, #27, #28, #29 |
| During SAD (general drafting, no section-blocking urgency) | 10 | #1, #3, #7, #8, #15, #16, #21, #24, #26, #30 |
| Implementation Phase | 6 | #5, #10, #11, #18, #20, #22 |
| After SAD / Future Release | 2 | #13, #31 |

**13 + 10 + 6 + 2 = 31.** Matches the per-row table exactly.

**No question requires resolution before SAD work starts.** This
matches every prior readiness assessment in this repository exactly —
the 13 section-finalization-blocking items (including both Critical
items, #4 and #14) block *finalizing* specific sections once SAD work
is underway, not the SAD phase's ability to begin. Of these 13, only 6
rise to the status of a **formal Certification Condition** on this
audit's PASS WITH CONDITIONS verdict — see `18-CERTIFICATION-REPORT.md`
for exactly which 6 and why the other 7 (plus non-Open-Question items
like R-08 and R-01) are tracked as SAD-input dependencies without being
elevated to formal conditions.

## Explicit Reminder (updated 2026-07-18)

18 of the 31 questions were resolved in the Open Questions Resolution
phase using existing repository evidence, architecture principles, and
enterprise best practice — per `20-OPEN-QUESTIONS-RESOLUTION.md`, none
by inventing a business, legal, or clinical fact. The remaining 13 stay
correctly unresolved here: genuine Legal, Regulatory, and Country
Localization dependencies remain the province of the user, business
stakeholders, or formal legal counsel, none of which this Board is —
the No-Guessing Rule (CLAUDE.md §3) was not relaxed for this phase.
