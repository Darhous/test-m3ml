# Consolidated Open Questions Register

All 31 Open Questions from `.claude/context/open-questions.md`,
classified by priority and by when resolution is actually required.
Classification is this audit's own judgment, applied consistently
against one criterion: **does the SAD need this answered to start, to
finish a specific section, or can it wait past SAD entirely?** No
question is closed here — closing any of these requires product/
business/legal authority this Board does not hold, consistent with
every prior phase's own restraint.

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

## Explicit Reminder

Per `.claude/context/open-questions.md`'s own closing note and this
project's No-Guessing Rule (CLAUDE.md §3): **no answer is assumed for
any question above.** This register's contribution is prioritization
and timing classification only — the substantive answers remain
entirely the province of the user, product/business stakeholders, or
formal legal counsel, none of which this Board is.
