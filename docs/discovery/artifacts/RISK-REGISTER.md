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

*(Populated as Discovery proceeds. Severity is qualitative — High/Medium/
Low with stated reasoning — per the No-Guessing Rule; no numeric risk
scoring is invented without a real basis.)*
