# Candidate Modules and Platform Services (Wave 10)

**Status: Draft.** Derived **from** Wave 9's 28 Bounded Contexts (per the
user's explicit instruction — modules from contexts, not the reverse).
Every module traces to exactly one Bounded Context, consistent with
Constitution Section 8 (One Owning Module Per Bounded Context Concept),
already Accepted.

## Classification Legend

**Core Platform Service** = Constitution Section 10's Core Platform
(universal dependency). **Independent Gateway** = Constitution Section 11
Independent Component. **Shared Technical Service** = cross-cutting,
read-mostly, serves all Business Modules without being a dependency they
require to function. **Business Module** = owns one domain's data/rules.
**Commercial Module** = SaaS-commercial-specific, distinct lifecycle from
clinical/operational Business Modules.

## Module Catalog

| Module | Classification | Owns (from Wave 9) | Key Dependencies | Extraction Trigger (Constitution Section 55) | Evidence |
|---|---|---|---|---|---|
| Identity and Access | Core Platform Service | Context 27 | None (universal dependency) | N/A — Core Platform, not extraction-eligible by default | Evidenced |
| Tenant and Organization Management | Core Platform Service | Context 26 | None | N/A | Evidenced |
| Audit and Compliance | Core Platform Service | Context 28 | None | N/A | Evidenced |
| Device Integration Gateway | Independent Gateway | Context 9 | Core Platform (contract-only) | Already independent (ADR 0006) | Evidenced |
| Notification Service | Independent Gateway | Context 21 | Core Platform | Already independent (Constitution Section 11) | Evidenced |
| AI Operations Gateway | Independent Gateway | Context 24 | Core Platform | Already independent (ADR 0007) | Evidenced |
| Analytics | Shared Technical Service | Context 23 | Reads all Business Modules (Open Host Service) | Measured query-load justifying a dedicated Analytics Platform (Constitution Section 55, already-Accepted trigger type) | Evidenced (Wave 5) |
| Document Management | Shared Technical Service | Context 22 | Core Platform | N/A yet — 0 real evidence | Inferred only |
| Patient Management | Business Module | Context 1 | Core Platform | Sustained scaling need (Section 55) | Evidenced |
| Practitioner and Clinic Management | Business Module | Context 2 | Core Platform, Patient Management | Sustained scaling need | Evidenced |
| Scheduling and Encounters | Business Module | Context 3 | Patient Mgmt, Practitioner Mgmt | Sustained scaling need | Evidenced |
| Diagnostic Ordering | Business Module | Context 4 | Core Platform | Sustained scaling need | Evidenced (Baseline) |
| Specimen Operations | Business Module | Context 5 | Diagnostic Ordering | Sustained scaling need | Evidenced (Baseline) |
| Laboratory Execution | Business Module | Context 6 | Specimen Operations, Device Integration (ACL) | Measured need (device-load-driven, per Constitution Section 55's Search/Cache trigger pattern applied here) | Evidenced (Baseline) |
| Result Verification and Reporting | Business Module | Context 7 (**Core**) | Laboratory Execution, Specimen Operations | Extraction discouraged by default — Core Domain modules stay in the Monolith longest per ADR 0001's own reasoning, extracted only on strong measured need | Evidenced (Baseline) |
| Quality Management | Business Module | Context 8 | Laboratory Execution, CRM (Complaint→CAPA link) | Sustained scaling need | Evidenced (Wave 5) |
| Asset and Maintenance | Business Module | Context 10 | Device Integration | Sustained scaling need | Evidenced (Wave 5) |
| Inventory | Business Module | Context 11 | Laboratory Execution (consumption) | Sustained scaling need | Evidenced (Wave 5) |
| Procurement | Business Module | Context 12 | Inventory, Supplier Management | Sustained scaling need | Evidenced (Wave 5) |
| Supplier Management | Business Module | Context 13 | Procurement | Sustained scaling need | Evidenced (Wave 5) |
| Billing | Business Module | Context 14 | Diagnostic Ordering, Result Verification (event) | Sustained scaling need | Evidenced (Baseline) |
| Payments and Treasury | Business Module | Context 15 | Billing (Partnership pattern) | Sustained scaling need | Evidenced (Wave 5) |
| Insurance and Corporate Contracts | Business Module | Context 16 | Billing, external Payer (ACL) | Sustained scaling need | Evidenced (Baseline + Wave 5) |
| Accounting | Business Module (Generic, Integration-leaning per Wave 3) | Context 17 | Payments and Treasury, Expenses | **Most extraction-ready by default** — Wave 3 already recommended Integration-capable over deep-native, making this the first candidate for an external-system boundary rather than a Monolith module, pending real product decision | Evidenced (Wave 5) |
| Workforce Management | Business Module (Generic) | Context 18 | Core Platform | Sustained scaling need | Evidenced (Wave 5) |
| Payroll | Business Module (Generic, high sensitivity) | Context 19 | Workforce Management | Regulatory/compliance-driven trigger (e.g., a jurisdiction requiring payroll data residency) more likely than a scaling trigger | Evidenced (Wave 5) |
| CRM and Support | Business Module (Generic) | Context 20 | Patient/Practitioner Mgmt (read) | Sustained scaling need | Evidenced (Wave 5) |
| SaaS Commercial Operations | Commercial Module | Context 25 | Tenant and Organization Management | Sustained scaling need | Evidenced (Wave 5) |

## Optional Add-ons (Recommended, not yet justified by real demand)

Predictive Maintenance (Wave 3, Category 6 — explicitly flagged
speculative), advanced BI/Forecasting depth beyond basic Analytics,
Marketplace Readiness (Wave 1 — flagged speculative). None of these are
modules yet — they are capabilities that could become Optional Add-on
modules once real demand is confirmed, listed here so they are not lost,
not because they are committed.

## Market-Specific Modules

**None yet identifiable** — Wave 11 (Egypt Market Gap Analysis) is the
correct place to determine whether any Egypt-specific requirement rises to
the level of a distinct module (e.g., a dedicated e-invoicing-compliance
module) versus a configuration of an existing module (e.g., Accounting).
Not pre-judged here.

## Tenant-Specific Extensions

**Mechanism not chosen** (consistent with Wave 1's deferral of the
specific entitlement/metering mechanism to the SAD). White-labeling and
tenant-specific custom fields are Confirmed *requirements* (Wave 1) but
not yet modeled as a specific extension mechanism — flagged for the SAD,
not designed here.

## Domain Core vs. Platform Kernel vs. Shared Infrastructure — Explicit Distinction

| Layer | Members | Why This Layer |
|---|---|---|
| **Domain Core** | Result Verification and Reporting (and, per Wave 7's recommendation, its orchestration relationship to Laboratory Execution/Specimen Operations/Diagnostic Ordering) | Where competitive differentiation lives (Wave 7) |
| **Platform Kernel** | Identity and Access, Tenant and Organization Management, Audit and Compliance | Universal dependency, never itself a Business Module (Constitution Section 10) |
| **Shared Infrastructure** | Device Integration Gateway, Notification Service, AI Operations Gateway | Independent Components (Constitution Section 11) — infrastructure-shaped but domain-adjacent |
| **Cross-Cutting Services** | Analytics, Document Management | Serve all Business Modules without being required by them to function |
| **Business Modules** | The remaining 19 contexts | Domain-specific, each independently extractable per Constitution Section 55's evidence-based triggers |

## Traceability Confirmation

Every module above traces to exactly one Wave 9 Bounded Context, which in
turn traces to specific Wave 3 Capabilities and Wave 5 Events (or is
explicitly marked `Inferred only` where that chain is incomplete —
Document Management is the sole such case). No module was invented
independently of this chain.
