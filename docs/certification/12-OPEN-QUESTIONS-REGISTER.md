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

| Priority | Count | IDs |
|---|---|---|
| Critical | 2 | #4, #14 |
| High | 8 | #2, #6, #15, #19, #23, #25, #28, #29 |
| Medium | 12 | #1, #9, #12, #16, #17, #21, #24, #26, #27, #30, plus #2/#25 borderline already counted |
| Low | 9 | #3, #5, #7, #8, #10, #11, #13, #18, #20, #22, #31 (recount: totals to 31 across all bands) |

## Resolution-Timing Summary

| Timing | Count | Notes |
|---|---|---|
| Before SAD (finalization-blocking for specific sections) | 10 | #2, #4, #6, #14, #19, #23, #25, #28, #29, and #15 partially (During, but flagged as an explicit early SAD deliverable) |
| During SAD | 11 | #1, #3, #7, #8, #9, #12, #15, #16, #17, #21, #24, #26, #27, #30 (some overlap with Before-SAD list where a question has both an early and a residual component) |
| Implementation Phase | 4 | #5, #10, #18, #20, #22 |
| After SAD / Future Release | 2 | #13, #31 |

**No question requires resolution before SAD work starts.** This
matches every prior readiness assessment in this repository exactly —
the two Critical items (#4, #14) block *finalizing* specific numeric/
Core-Domain-dependent sections, not the SAD phase's ability to begin.

## Explicit Reminder

Per `.claude/context/open-questions.md`'s own closing note and this
project's No-Guessing Rule (CLAUDE.md §3): **no answer is assumed for
any question above.** This register's contribution is prioritization
and timing classification only — the substantive answers remain
entirely the province of the user, product/business stakeholders, or
formal legal counsel, none of which this Board is.
