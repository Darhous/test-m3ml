# Discovery Risk Register

**Purpose:** risks identified during Discovery (business, domain-modeling,
security, integration, AI, tenancy) that are not yet — and may never be —
Constitution-level Risk Governance entries (Constitution Section 58 governs
platform risk categories generally; this register is Discovery-phase-
specific and feeds candidates into that framework, it does not replace it).

| # | Risk | Category | Phase Identified | Severity (qualitative) | Notes |
|---|---|---|---|---|---|
| 1 | Entire Capability Map/Value Stream set rests on industry-reference assumption rather than confirmed input | Business | 02 | Medium | Mitigated by explicit tagging; must be user-reviewed before SAD work. |
| 2 | Insurance/billing model unknown while VS4 was fully traced around it | Business | 02 | Low-Medium | VS4 intentionally shallow; see open-questions.md #17. |
| 3 | No event modeled for mid-processing equipment failure (H2) — a real gap in failure-mode coverage, not yet a business rule | Operational | 03 | Medium | Directly relevant to Constitution Section 24 (device failure must not corrupt core data) — must be closed by Phase 07/08, not left open into Phase 12. |
| 4 | Result-verification authority (H1) is unresolved while `ResultVerified` is already flagged a candidate Sensitive Operation | Governance/Clinical | 03 | Medium-High | Ties directly to Constitution Section 21 (elevated controls for sensitive operations) — a wrong authority model here has real clinical-safety implications; prioritize for Phase 07. |
| 5 | 3 Subdomains (Inventory, QC/Accreditation, Staff/Operations) classified on capability-list evidence alone, no Event Storming evidence | Domain-Modeling | 04 | Medium | If Phase 06 draws Bounded Context boundaries around these without better evidence, the boundaries may need rework once real business input arrives. |
| 6 | Core Domain proposal has a credible competing alternative (Specimen Management/Home Collection) not resolved by evidence available in this session | Business/Strategic | 04 | Medium | Directly affects where the "deepest modeling investment" should go later — must be confirmed by the user, not decided by Discovery alone. |
| 7 | Patient and Doctor have no distinct Bounded Context — remain cross-context Actors only | Domain-Modeling | 06 | Low-Medium | May be correct (they are genuinely cross-cutting), or may indicate a missing "Patient Profile"/"Doctor Profile" context not yet evidenced — flagged for Phase 07/11, not resolved here. |
| 8 | Billing and Claims context built on the weakest Value Stream (VS4) is now a formal Bounded Context with real Module Ownership implications | Business/Domain-Modeling | 06 | Medium | If `open-questions.md` #17 resolves very differently than assumed, this context's boundary (not just its internal rules) may need rework, not just a rule update. |
| 9 | Billing/Claims operations classified as NOT meeting the Sensitive Operation bar (Constitution Section 21) | Governance | 07 | Low-Medium | Defensible per the Constitution's literal definition, but worth a second look in Phase 11 — some jurisdictions treat financial-medical linkage data as sensitive too; not resolved here, just flagged. |
| 10 | 5 of 10+ resolved Hotspots still have fully Open business-level thresholds (expiry window, escalation N, retry policy) baked into an otherwise-fixed rule *shape* | Domain-Modeling | 07 | Medium | The rule shapes are sound, but if real values differ wildly from typical industry ranges, the shape itself (not just a config number) could need rework — flagged for Phase 11 re-check. |
| 11 | Every candidate Aggregate is missing explicit Tenant-scoping fields | Domain-Modeling/Security | 09 | Medium-High | Not a design flaw (Phase 05 was tactical-modeling-focused, tenancy is layered on per standard DDD sequencing) but must not be forgotten heading into the SAD — Constitution Section 18 is unambiguous that this is Required, not optional. |
| 12 | Invoice's `Amount` field has no currency; `DeviceImportRecord`'s timestamp has no timezone context | Localization | 09 | Medium | Direct gap against Constitution Section 32 (Accepted, ADR 0010) — proposed fixes exist (`09-tenancy-analysis.md`) but are not yet applied to the Aggregate definitions themselves. |
| 13 | Use Case #8 (AI notification summarization) is Permitted per Section 28's literal list but risky in practice (free-form generation to a patient with no accuracy check) | Clinical/AI Governance | 10 | Medium-High | The Constitution's Forbidden list doesn't explicitly cover this scenario — a real gap between "technically permitted" and "actually safe" that Phase 11/12 should treat seriously, not wave through because it passed the literal Forbidden-list check. |
| 14 | Denial of Service / abuse via unthrottled requests (SEC-01) | Security/Platform | Gap Closure Wave 12 | High | Carried-forward Constitution-level Open Risk (REVIEW-REPORT.md R1) — not closed by Discovery. Full Cause/Mitigation/Detection/Escalation/Residual detail in `W12-security-privacy-clinical-safety-register.md`. |
| 15 | Security/privacy breach with no defined incident-response process (SEC-02) | Security/Platform | Gap Closure Wave 12 | High | Carried-forward Constitution-level Open Risk (REVIEW-REPORT.md R2). Compounds Wave 11's PDPL finding. See W12 register. |
| 16 | Break-Glass override used as routine bypass rather than exception (SEC-03) | Governance/Identity | Gap Closure Wave 12 | Medium-High | Carried-forward Constitution-level Open Risk (v1 REVIEW-REPORT R5) — policy Accepted (Section 21), technical enforcement mechanism still SAD-level. See W12 register. |
| 17 | Cross-tenant data leakage via the shared-tier isolation mechanism (SEC-04, consolidated with SEC-08) | Security/Tenancy | Gap Closure Wave 12 | **Highest** | Isolation technique still undecided (Wave 9 open item #15). Mitigation floor: Constitution Section 36 Multi-Tenant Isolation Testing (mechanism-agnostic). Blocks module acceptance until resolved. See W12 register. |
| 18 | AI notification summarization (Use Case #8) reaches a patient without human review (SEC-05, restates Baseline Risk #13 with an explicit escalation flag) | Clinical/AI Governance | Gap Closure Wave 12 | Medium-High | Flagged for user decision at Wave 14 as a possible Constitution Amendment candidate (Section 45). See W12 register. |
| 19 | Device failure and replay attack — a captured device message resubmitted to duplicate/falsify a result (SEC-06) | Security/Device Integration | Gap Closure Wave 12 | High | New finding. Mitigation: apply the existing Idempotency Policy (Constitution Section 48) specifically at device-message ingestion — not yet confirmed implemented. See W12 register. |
| 20 | Unauthorized result verification — a non-eligible actor performs `ResultVerified` (SEC-07) | Clinical/Governance | Gap Closure Wave 12 | **Highest** | Floor mitigation (Role gate) is Evidenced; full closure depends on `open-questions.md` #19, the single highest-priority open item in the project. See W12 register. |
| 21 | Financial manipulation — unauthorized invoice/refund alteration, fraudulent discount application (SEC-09) | Security/Financial | Gap Closure Wave 12 | Medium-High | New finding. Reduced once the Elevated-Audit-tier question (`open-questions.md` #24) is resolved. See W12 register. |
| 22 | Payroll data leakage (SEC-10) | Security/Workforce | Gap Closure Wave 12 | High | New finding. Recommended mitigation: apply the existing medical-data Data Scope pattern (Constitution Section 21) to Payroll. Ties to Wave 11's Labor Law gap (`open-questions.md` #26). See W12 register. |
| 23 | Inventory fraud — stock adjustment bypassing reason code, or collusive over-ordering (SEC-11) | Security/Supply Chain | Gap Closure Wave 12 | Medium | New finding. Partially reduced by existing BR-INV01 reason-code rule; full closure needs a periodic audit process (SAD-level, not yet designed). See W12 register. |
| 24 | Supplier collusion — a Supplier and an internal actor coordinate to defraud procurement (SEC-12) | Security/Supply Chain | Gap Closure Wave 12 | Medium | New finding. Recommended mitigation: segregation-of-duties (PO issuer ≠ approver ≠ receiver), not yet Confirmed as a Constitution-level rule. See W12 register. |
| 25 | Audit tampering — an actor with elevated access attempts to alter/delete an Audit Event (SEC-13) | Security/Audit | Gap Closure Wave 12 | **Highest** | Mitigation (append-only enforcement, Constitution Section 23) already Accepted; this Wave adds the explicit threat framing. Undermines every other mitigation in this register if it fails. See W12 register. |

*(Populated as Discovery proceeds. Severity is qualitative — High/Medium/
Low with stated reasoning — per the No-Guessing Rule; no numeric risk
scoring is invented without a real basis.)*

## Gap Closure Wave 12/13 — Security, Privacy, Clinical Safety Merge

Rows #14–25 above are the Wave 12 security/privacy/clinical-safety register
(`W12-security-privacy-clinical-safety-register.md`), merged into this
canonical table at Wave 13 (Validation) per that Wave's design. SEC-08 was
**not** re-added as a separate row — it was Wave 12's own consolidation of
a duplicate framing of SEC-04 (same root cause: shared-tier isolation
mechanism undecided), so merging it separately here would have
re-introduced the exact risk-count-drift problem Wave 0 fixed. Register
total after merge: **25 rows** (13 Baseline + 12 Gap Closure), 3 rated
**Highest** severity (#17 cross-tenant leakage, #20 unauthorized
verification, #25 audit tampering) — all three tie to foundational trust
guarantees rather than any single domain. Full Cause/Detection/Escalation/
Residual/Evidence/Status detail for rows #14–25 remains in the W12
artifact; this table's simpler 5-column schema summarizes rather than
duplicates it.
