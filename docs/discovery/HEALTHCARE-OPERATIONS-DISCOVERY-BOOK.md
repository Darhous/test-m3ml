# Healthcare Operations Discovery Book — Egypt-First Platform

**Status:** Baseline Complete — Stakeholder Validation Pending.

This is the Gap Closure Program's final Discovery baseline, synthesizing
the original 12-phase Baseline Discovery (Laboratory-Operations-focused)
and the 15-Wave Discovery Gap Closure & Healthcare Operations Platform
Expansion program (Waves 0–14) into one coherent document. It supersedes
`docs/discovery/DISCOVERY-BOOK.md` as the current Discovery baseline — the
old book is marked Superseded, not deleted (Section 41 below explains why
and where each part of it now lives).

**This is not a Software Architecture Document, an API/Database/
Deployment Design, a Technology/Framework/Cloud Selection, Production
Code, a Module SDK/Template, or an Execution Roadmap.** It does not
authorize starting any of those. See Section 42.

---

## 1. Executive Summary

The platform's confirmed direction is a **Healthcare Operations Platform**
— broader than a Laboratory Information Management System, Patient
Portal, or Billing System alone — with **Egypt as the first target
market** and architecture readiness for future markets. It serves 9
customer types across 32 business domains, through a central backend with
unified login and role/permission/data-scope/organization/branch-based
routing to the right Portal/Dashboard. The Baseline Discovery (12 phases)
produced a Laboratory-Operations-scoped candidate model: 20 capabilities,
4 value streams, 26 domain events, 8 Bounded Contexts, 2 Proposed ADRs.
The Gap Closure program (Waves 0–13, this document is Wave 14) expanded
that model to enterprise scope without discarding it: 100 capabilities,
20 value streams, ~114 domain events, a 28-context Hybrid Modeled/
Recognized Bounded Context map, a 25-row consolidated Risk Register, a
36-row Assumption Register, and a 27-item canonical Open Questions
register (24 tracked at Discovery-local granularity). Every expansion
claim not directly Confirmed by the user is explicitly tagged `Inferred —
Industry Reference`, `Recommended`, or `Requires Legal Verification` —
never asserted as settled fact, per the No-Guessing Rule
(`CLAUDE.md` Section 3).

## 2. How to Read This Book — Evidentiary Status Legend

- **Confirmed** — stated by the user, or already Accepted in
  `.claude/context/` / an Accepted ADR.
- **Recommended** — a professional judgment call this program makes
  explicitly, not yet decided by the user.
- **Inferred — Industry Reference** — standard healthcare/lab/financial/
  workforce operations practice, used to make Discovery executable without
  live stakeholder interviews, per the approved execution mode.
- **Requires Legal Verification** — a real, dated research finding about
  Egyptian law/regulation that is **not** a compliance claim and must not
  be treated as one until independently legally verified.

No item in this book is Accepted architecture. See Section 39
(Readiness) and Section 42 (Final Status) for exactly what remains before
any of it can be treated as settled.

## 3. Execution Mode and Governance Note

The Baseline Discovery ran under an approved **Assumption-Driven
Autonomous Run** (no live stakeholder access). The Gap Closure program
ran under an explicit **Executive Authorization**, scoped to this
repository, permitting file creation/editing/renaming/superseding (never
silent deletion of unmigrated knowledge), new/amended ADRs, and direct
commits to `main`, while excluding force-push, history deletion, Skill/
Plugin installation without approval, and any claim of final legal
compliance. Both modes are logged in full in
`docs/discovery/reports/00-discovery-program-status-report.md` (Baseline)
and `docs/discovery/reports/GAP-CLOSURE-00-BASELINE-AUDIT.md` (Gap
Closure) — not repeated here.

## 4. Vision and Mission

**Confirmed:** a digital healthcare platform starting from laboratory
management, growing into a broad, extensible healthcare platform — not a
plain CRUD system. **Recommended (Wave 1):** the mission statement
"orchestrate the patient-to-result journey and the operational backbone
around it, across any healthcare organization type, starting in Egypt."
Full detail: `.claude/context/vision.md`,
`docs/discovery/artifacts/W1-vision-scope-operating-model.md`.

## 5. Target Market — Egypt First, Future-Market Readiness

**Confirmed:** Egypt is the first target market; the architecture must
remain ready for future markets without being built specifically for any
of them yet. No other specific country is Confirmed as a future target —
that remains context item #1, still Open. See Section 26/27 for what was
actually researched about Egypt specifically.

## 6. Platform Vision — Healthcare Operations Platform

**Confirmed:** the product is a full Healthcare Operations Platform,
explicitly not just a LIMS, LMS, Patient Portal, or Billing System. It
supports Laboratory, Clinical, Workforce, Financial, Supply Chain,
Customer Operations, SaaS/Platform, and Governance operations under one
central backend with unified login and scoped routing. See Section 11
for the full 10-category, 100-capability breakdown.

## 7. Customer Types (9)

**Confirmed:** independent lab, lab chain, hospital, medical center,
clinic, medical group, corporate healthcare provider, multi-branch
diagnostic entity, partner/API client. **Recommended (Wave 1):** a
3-cluster grouping (Single-Facility / Multi-Facility-Chain / Ecosystem-
External) for capability-scoping purposes only, not a data model — see
Assumption Register #27.

## 8. Business Domains (32)

**Confirmed (user-named list):** 32 business domains spanning Clinical,
Laboratory Operations, Workforce, Financial, Supply Chain, Asset/Device,
Customer Operations, SaaS/Platform, and Governance. All 32 map to at
least one Enterprise Capability Map entry (Section 11) and 29 of 32 have
Event Storming coverage (Section 14) — the 3 without are the Egypt-
legal-gated items named in Section 40.

## 9. Operating Model Commitments

**Confirmed:** White Label, Plans/Subscriptions, Usage/Entitlement
Tracking, and SaaS billing readiness are required operating-model
commitments, not optional features. These directly informed the SaaS/
Platform capability category (Section 11) and the Commercial Module tier
(Section 25). Detail: `W1-vision-scope-operating-model.md`.

## 10. Stakeholders, Actors, and Personas (39)

Expanded from the Baseline's 15 stakeholder categories / 4 personas to
**39 named personas across 8 categories** (Clinical, Laboratory
Operations, Financial, Workforce, Supply Chain, Customer Operations,
Platform/SaaS, Governance), each with `Inferred` Goals/Pain Points/KPIs
(Assumption Register #28). One genuine open architectural tension
(Platform Operator/Support cross-tenant visibility vs. tenant isolation)
was surfaced and deliberately left for the Security review (Section 28),
not resolved here. Full catalog: `W2-persona-catalog.md`; original 4:
`.claude/context/stakeholders.md`.

## 11. Enterprise Capability Map (100 Capabilities, 10 Categories)

Rebuilt from the Baseline's 20 (Laboratory-only) capabilities to **100
across 10 categories**: Clinical, Laboratory Operations, Workforce,
Financial, Supply Chain, Asset/Device, Customer Operations, SaaS/
Platform, Governance, Data/Intelligence. Every one of the 32 Confirmed
business domains maps to at least one capability. 84 of 100 entries are
`Inferred` or `Confirmed-scope/Inferred-detail` (Assumption Register
#29). Full map: `W3-enterprise-capability-map.md`; category diagram:
`diagrams/W3-capability-map-categories.md`.

## 12. Financial Native/Integration/Deferred Boundary

**Recommended (Wave 3), directly per the user's explicit "no full ERP
assumed" instruction:** the Capability Map draws an explicit boundary
between Financial capabilities the platform builds **Natively**
(invoicing, patient billing, cashbox/point-of-collection payment),
capabilities it **Integrates** with (full General Ledger/Chart of
Accounts, tax filing, bank reconciliation feeds), and capabilities
explicitly **Deferred** (multi-currency treasury, complex payroll tax
calculation engines). This boundary is respected consistently through
the Bounded Context map (Section 22) and Candidate Modules (Section 24)
— re-verified at Wave 13 (Validation, Dimension 16: Pass).

## 13. Value Streams and Customer Journeys (20)

Expanded from the Baseline's 4 (VS1–VS4) to **20 Value Streams**; 18
newly traced with trigger/outcome/actors/domains/bottleneck, 2 mapped to
already-traced Baseline streams. Confirms Section 11's evidence-imbalance
finding independently. Full detail: `W4-value-streams-expanded.md`.

## 14. Domain Event Catalog

The Baseline's 26 events (+4 gap-identified) grew to **~114** after Wave
5 storm-walked 29 previously-missing business domains into 10 clusters
(~84 new events + 2 Timer-driven events). All new events are `Inferred —
Industry Reference` (Assumption Register #31). Full catalog:
`03-event-storming-board.md` (Baseline), `W5-event-storming-gap-closure.md`
(Gap Closure).

## 15. Patient and Doctor as Owned Domains

**Recommended (Wave 5), closing Baseline Risk #7:** Patient and Doctor
are modeled as owned domains with their own event chains for the first
time, not merely cross-cutting Actors. Wave 9 gives each a dedicated
Recognized-tier Bounded Context (Section 22). Whether they belong inside
the amended Core Domain ("Patient-to-Result Orchestration") or remain
separate is intentionally left open — see Section 36.

## 16. Business Rules and Policy Catalog

Extends the Baseline's business-rules/state-machine layer with a
**26-rule catalog across all 24 user-requested categories**, including a
second Sensitive-Operation-grade pattern (Payroll dual-control) alongside
the Baseline's Result Verification gate. All rules are `Inferred`
(Assumption Register #32); rule *shapes* are well-grounded in Constitution
Section 21/23/25/26, specific thresholds remain Open (`open-questions.md`
#23). Full catalog: `W6-business-rules-and-policy-catalog.md`.

## 17. Configurable Result Verification Policy Model

**The centerpiece of Wave 6**, per explicit user direction: Result
Verification is **not** governed by one fixed rule. The model varies
approval requirements across 8 context dimensions (organization type,
analysis type, risk level, specialty, approval level, role, branch,
country policy) plus emergency override, while every approval remains
Backend-enforced, Audited, Traceable, Versioned, and Configurable within
safe limits (never bypassable by configuration alone). This refines,
rather than contradicts, the Baseline's Result Verifier Role gate — the
gate is the enforcement floor; the Policy Model configures who meets it
in a given context. Actual axis values are explicitly not invented —
`open-questions.md` #23, tied to the single highest-priority open item
in the project (#19, Result Verifier eligibility criteria). Full model:
`W6-business-rules-and-policy-catalog.md`.

## 18. Elevated Audit Tier (Candidate)

**Recommended, not Confirmed (Wave 6):** a second, broader "Elevated
Audit" tier — beyond the Constitution's existing Sensitive Operations
category — covering Refund, Expiry-block, Break-Glass, and Tenant
Configuration actions. Tracked as `open-questions.md` #24, disposition
deferred to a future governance pass, not decided in this program.

## 19. Domain Classification — Core / Supporting / Generic / Platform

Wave 7 re-classified all domains (Baseline + Gap Closure) into Core/
Supporting/Generic/Platform tiers using DDD Strategic Design/Distillation.
"Platform Tenant Operations" was reasoned out as Platform-tier, not Core,
despite superficial centrality — it is necessary infrastructure, not
differentiating value. Full classification: `W7-domain-classification-
reevaluation.md`.

## 20. Core Domain Decision Matrix and Recommendation

Wave 7 built a 6-alternative Decision Matrix (original "Test Processing
and Result Verification," "Patient-to-Result Orchestration," "Laboratory
Execution," "Healthcare Operations Orchestration," "Clinical Diagnostic
Network," "Platform Tenant Operations") without assuming the Baseline's
answer was final. **Recommendation: "Patient-to-Result Orchestration."**
"Clinical Diagnostic Network" was rejected for having no supporting
evidence; "Healthcare Operations Orchestration" was rejected as premature
given the enterprise expansion's own evidence imbalance (Section 11).
This recommendation is formally reflected in ADR-0011's Amendment —
Section 36.

## 21. Ubiquitous Language and Glossary Governance

Wave 8 disambiguated **37 conflict-prone terms**, each pinned to its
owning Bounded Context with explicit Forbidden Synonyms; 6 terms were
rejected as standalone canonical terms. Surfaced 1 genuine domain gap
(Department, not yet modeled) and 1 unexercised naming decision (Batch
vs. Lot). Full glossary work: `W8-ubiquitous-language-expansion.md`;
canonical pointer: `.claude/context/glossary.md`.

## 22. Bounded Context Map — Modeled/Recognized Hybrid (28 Contexts)

Wave 9 remapped from the Baseline's 8 contexts to a **28-context Hybrid
map**: the original 8 (refined per Wave 8's naming work) plus 1 more
Evidenced context form the **Modeled tier (9 contexts)**; the remaining
**19 are Recognized-tier** — named and boundary-sketched from capability/
event evidence but explicitly lower-confidence (`Inferred`) and not yet
tactically modeled to Phase-05 depth. A 29th candidate (Integration Hub)
was rejected on evidence grounds. The acyclic Module Dependency graph
property holds across all 28. Full remap: `W9-bounded-context-
remapping.md`; diagram: `diagrams/W9-context-map-enterprise.md`. This is
formally reflected in ADR-0012's Amendment — Section 37.

## 23. Context Mapping Patterns Applied

Every one of the 28 contexts' relationships is pattern-labeled (Customer/
Supplier, Partnership, Conformist, Anti-Corruption Layer, Open Host
Service, Published Language, Shared Kernel, Separate Ways), consistent
with the Baseline's original 11-relationship map and Constitution
Section 7's guidance to keep Shared Kernel rare and small. No new pattern
type was introduced beyond the Baseline's established set. Detail:
`W9-bounded-context-remapping.md`.

## 24. Candidate Modules and Platform Services (28)

Wave 10 derived **28 candidate modules strictly from Wave 9's Bounded
Contexts** (contexts first, modules second — never the reverse), tracing
each module back to specific Wave 3 capabilities and Wave 5 events. Full
catalog: `W10-candidate-modules-platform-services.md`.

## 25. Module Classification

Modules are classified into **Core Platform Services**, **Independent
Gateways**, **Shared Technical Services**, **Business Modules**, and
**Commercial Modules**. Accounting is flagged as most extraction-ready by
default (clean boundary, standard integration pattern); Result
Verification and Reporting (Core) is confirmed least likely to ever
extract, consistent with Constitution Section 55's evidence-based
extraction-trigger philosophy — no extraction timeline or number is
invented.

## 26. Egypt Market Gap Analysis (21 Considerations)

Wave 11 addressed all 21 user-requested Egypt-market considerations,
each explicitly typed (Legal/Regulatory, Industry Practice, Product
Recommendation, or Architectural Inference — never a bare compliance
claim). 7 items (considerations #6, #7, #14, #16-partial, #18, #19, #20,
#21) are `Industry Practice`/`Product Recommendation`, not independently
researched this round (Assumption Register #35). Full analysis:
`W11-egypt-market-gap-analysis.md`.

## 27. Egypt Regulatory Research Register

4 real, dated regulatory topics were researched via live web search:
ETA e-invoicing/e-receipt mandate (Resolution 281/2025), Personal Data
Protection Law (151/2020), Egyptian Drug Authority device/reagent
registration (Decisions 153/2025, 161/2025), and the Universal Health
Insurance Law (2/2018). Every finding is tagged `Requires Legal
Verification` — none is a compliance claim. Register with sources/dates:
`EGYPT-REGULATORY-RESEARCH-REGISTER.md`.

## 28. Security, Privacy, and Clinical Safety Risk Review

Wave 12 produced a 12-risk register (STRIDE-categorized) covering all 13
user-named risk categories (1 pair consolidated as duplicate framings of
the same underlying risk — SEC-04/SEC-08, cross-tenant leakage). 5 risks
are carried-forward Constitution-level Open Risks (none closed by
Discovery, since Discovery cannot itself implement a policy or process);
7 are newly surfaced across Device/Verification/Financial/Payroll/
Inventory/Supplier/Audit domains. 3 rated **Highest** severity, all
tying to foundational trust guarantees (tenant isolation, audit
immutability, clinical authorization). Merged into the consolidated Risk
Register at Wave 13 — see Section 33. Full register:
`W12-security-privacy-clinical-safety-register.md`.

## 29. AI Governance

AI remains a governed operational layer per Constitution Section 28: it
may never independently approve or modify results, issue diagnoses, send
final medical decisions, bypass permissions, or expose sensitive data
externally without approved policy. The Baseline's 7 accepted + 1
rejected + 1 not-ready AI use case catalog (`10-ai-use-case-catalog.md`)
stands; the "not-ready" case (free-form notification summarization
reaching a patient without review) is carried forward as Risk Register
row #18 (SEC-05) and flagged for a possible Constitution Amendment
candidate at a future governance pass, not resolved by this program.

## 30. Multi-Tenancy and Localization

The Baseline's Hybrid Tenant Isolation model (ADR 0005, Accepted) and
Localization gap analysis (Money/timestamp Value Object gaps, Constitution
Section 32) stand unchanged. The shared-tier partitioning technical
detail (tenant-ID-column vs. schema-per-tenant) remains genuinely Open
(`open-questions.md` #15) and is the direct cause of Risk Register row
#17 (SEC-04, Highest severity) — the single most consequential unresolved
technical question carried into this baseline.

## 31. Workforce Domain

Payroll was identified (Wave 2) as "among the most sensitive non-clinical
data in the platform," given a dual-control business rule (Waves 5/6),
and a dedicated security risk (SEC-10, Risk Register row #22) tying it to
Egypt's Labor Law/Social Insurance gap (`open-questions.md` #26, entirely
unresearched this round — an explicit gap, not an assumption).

## 32. Supply Chain Domain

Inventory, Procurement, and Supplier Management each have Capability
(Section 11), Event (Section 14), Business Rule (Section 16), and Risk
(Section 28) coverage, cross-verified consistent at Wave 13 (Validation
Dimension 18: Pass) — e.g., the BR-INV01 reason-code rule, the
`StockCountDiscrepancyFound` event, and SEC-11/SEC-12 risks all
reference the same underlying control.

## 33. Consolidated Risk Register (25 Risks)

The canonical `RISK-REGISTER.md` now holds **25 rows**: the Baseline's 13
(business/domain-modeling/governance/localization/AI risks) plus 12
merged from Wave 12 (Gap Closure Wave 13's merge, rows #14–25). 3 rows
are rated **Highest** severity (#17 cross-tenant leakage, #20
unauthorized result verification, #25 audit tampering) — all three tie to
foundational trust guarantees rather than any single domain. Full
register: `RISK-REGISTER.md`.

## 34. Consolidated Assumption Register (36 Assumptions)

The canonical `ASSUMPTION-REGISTER.md` now holds **36 rows**: the
Baseline's 26 plus 10 consolidated entries (Gap Closure Wave 13, rows
#27–36) representing Waves 1, 2, 3, 4, 5, 6, 7, 9, 11, and 12's deferred
assumptions — logged per-Wave/category rather than per-individual-item,
to keep the register usable. Nothing in this register is Accepted project
fact. Full register: `ASSUMPTION-REGISTER.md`.

## 35. Consolidated Open Questions Register

The Discovery-local `OPEN-QUESTIONS-REGISTER.md` now holds **24 rows**,
reconciled at Wave 13 against the canonical `.claude/context/
open-questions.md`, which remains the authoritative **27-item** register.
The single highest-priority item across the entire program remains item
#19 (Result Verifier Role eligibility criteria) — directly compounded by
item #23 (Policy Model axis values, Section 17). Items #1–13 not
specifically advanced by any Gap Closure Wave (target markets beyond
Egypt, legal requirements broadly, hosting model, usage scale, device
types, currencies/languages, legacy systems) remain genuinely Open, not
fabricated closed.

## 36. ADR Disposition — ADR-0011 (Core Domain)

**Disposition: Amend.** `docs/adr/0011-core-domain-test-processing-and-
result-verification.md` is amended (Gap Closure Wave 14) to recommend
**"Patient-to-Result Orchestration"** as a broader reframing of the
original "Test Processing and Result Verification" proposal, per Wave 7's
Decision Matrix (Section 20). Status remains **Proposed — Amended**, not
Accepted — the amendment is itself `Inferred`-evidenced, not stakeholder-
confirmed. The original Decision, Alternatives, and Consequences sections
are preserved unchanged as historical record; the Amendment section is
additive, not a rewrite.

## 37. ADR Disposition — ADR-0012 (Bounded Context Map)

**Disposition: Amend.** `docs/adr/0012-candidate-bounded-context-map.md`
is amended (Gap Closure Wave 14) to recommend the **Hybrid Modeled (9)/
Recognized (19) 28-context map** in place of the original 8-context
proposal, per Wave 9's Decision Matrix (Section 22). Status remains
**Proposed — Amended**, not Accepted. The original 8 contexts survive
unchanged in substance within the Modeled tier; the original ADR content
is preserved as historical record, with the Amendment section additive.

## 38. Validation Summary — 20 Completeness Dimensions

Gap Closure Wave 13 ran all 20 user-specified completeness-dimension
checks (Completeness, Consistency, DDD quality, Terminology consistency,
Event completeness, Actor completeness, Policy completeness, Capability
completeness, Context coherence, Module traceability, Security coverage,
Risk ownership, Assumption coverage, Open question coverage, SaaS
coverage, Finance coverage, Workforce coverage, Supply chain coverage,
Patient and doctor coverage, Egypt market coverage): **18 Pass, 2
Partial** (both honestly named residual gaps, not defects — see Section
40), **0 Fail**. No recursive repair loop was triggered. Full detail:
`W13-validation-and-recursive-repair.md`.

## 39. Multi-Axis Readiness Assessment

**Deliberately not collapsed into one number**, per explicit instruction:

| Axis | Assessment |
|---|---|
| Process Completeness | High — all 13 Baseline phases + Waves 0–14 complete |
| Evidence Confidence | Medium — mixed by design, correctly tagged throughout |
| Stakeholder Confirmation | Low — nothing yet reviewed by the user (expected at this stage) |
| Governance Cleanliness | High — no silent ADR promotion, No-Guessing Rule held throughout |
| Domain Coverage | High — 32/32 capability coverage, 29/32 event coverage |
| Risk Coverage | Medium-High — 25-row register, 2 named residual gaps |
| Architecture Readiness | **Not Ready — By Design** — this is Discovery, not Architecture |

Full basis for each axis: `W13-validation-and-recursive-repair.md`.

## 40. Known Residual Gaps

Named honestly rather than papered over (Wave 13):

1. **3 of 32 business domains have no Event Storming coverage** — all 3
   are Egypt-market-only regulatory considerations still `Requires Legal
   Verification` (e-invoicing submission specifics, cross-border transfer
   mechanics, National ID linkage). Appropriately un-stormed until the
   underlying legal facts are known.
2. **Customer Operations and Data/Intelligence (Analytics) capability
   categories have no dedicated Wave 12 security risk entry.** Not
   retroactively fabricated — flagged for a future, explicitly-scoped
   security pass.

Both gaps are scope boundaries, not defects, and were not force-closed by
inventing content to satisfy a checklist.

## 41. Superseded Content and Change History

`docs/discovery/DISCOVERY-BOOK.md` (the original, Laboratory-Operations-
scoped book) is marked **Superseded** by this document as of Gap Closure
Wave 14 (2026-07-16) — **not deleted**. Every finding in the old book
remains valid within its original Laboratory-Operations scope and is
carried forward into the corresponding section of this book (old Section
2 Business Context → this book's Sections 11/13/14; old Section on
Bounded Contexts → this book's Section 22's Modeled tier; old ADRs 0011/
0012 → this book's Sections 36/37). The complete file-by-file history of
every creation, expansion, and this supersession is in
`docs/discovery/artifacts/DISCOVERY-CHANGE-MANIFEST.md`; the Wave-level
narrative is in `docs/discovery/GAP-CLOSURE-CHANGELOG.md`.

## 42. Final Status and Next Steps

**Status: Baseline Complete — Stakeholder Validation Pending.**

This program executed Discovery Gap Closure only. It explicitly did
**not** produce, and this book does not authorize:
- A Software Architecture Document
- Detailed API, Database, or Deployment Design
- Technology, Framework, or Cloud Selection
- Production Code
- A Module SDK or Template
- An Execution Roadmap

**Next step is user review**, specifically: the two Amended ADRs
(Sections 36–37), the highest-priority Open Question (#19, Result
Verifier eligibility, Section 17), the 3 Highest-severity risks (Section
33), and the Known Residual Gaps (Section 40). No Software Architecture
work should begin until that review occurs and the relevant ADRs are
formally promoted per Constitution Section 39/45 — not silently, and not
by continuing this program past this point.
