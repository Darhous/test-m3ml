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

*(Populated as Discovery proceeds. Severity is qualitative — High/Medium/
Low with stated reasoning — per the No-Guessing Rule; no numeric risk
scoring is invented without a real basis.)*
