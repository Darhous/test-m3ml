# Bounded Context Remapping (Wave 9)

**Status: Draft.** Rebuilds the Context Map from the Baseline's 8 contexts
to 28, using Wave 3 (Capabilities), Wave 5 (Events), and Wave 7 (Domain
Classification) as evidence — not committing to all 28 by default; see the
Decision Matrix for a real Retain/Expand/Hybrid choice.

## The 28 Candidate Bounded Contexts, Justified

| # | Context | Owns (Aggregates/Concepts) | Justification (business language / ownership / lifecycle) | Classification | Evidence |
|---|---|---|---|---|---|
| 1 | Patient Management | Patient, Guardian, Consent | Distinct lifecycle (registration→ongoing relationship), own Ubiquitous Language (Wave 8), now has owned events (Wave 5 Cluster G) | Core-adjacent | Evidenced (Wave 5) |
| 2 | Practitioner and Clinic Management | Practitioner, Doctor, Clinic Administrator record | Distinct actor lifecycle from Patient; credential verification is a distinct invariant | Supporting | Evidenced (Wave 5) |
| 3 | Scheduling and Encounters | Appointment, Encounter | Own state machine (Booked→Rescheduled→Cancelled / Started→Completed), distinct from Order lifecycle | Supporting | Evidenced (Wave 5) |
| 4 | Diagnostic Ordering | TestOrder, TestCatalogEntry | **Renamed from Baseline's "Order Management"** — same Aggregate, evidence carried forward unchanged | Supporting | Evidenced (Baseline) |
| 5 | Specimen Operations | Specimen, ChainOfCustodyRecord | **Renamed from "Specimen Management"** — unchanged evidence | Supporting (debated, per ADR 0011 discussion) | Evidenced (Baseline) |
| 6 | Laboratory Execution | *(processing sub-slice)* | Splits from the Baseline's single "Test Processing" context — the *analytical execution* step specifically | Core (per Wave 7 recommendation, as part of "Patient-to-Result Orchestration") | Evidenced (Baseline) |
| 7 | Result Verification and Reporting | TestResult, VerificationRecord | The *clinical sign-off and reporting* step — split from Laboratory Execution because its authorization/audit weight (Sensitive Operations) is categorically different from raw processing | **Core** | Evidenced (Baseline) |
| 8 | Quality Management | NonConformance, CAPA | New — regulatory/quality lifecycle distinct from clinical execution | Supporting | Evidenced (Wave 5, Cluster D) |
| 9 | Device Integration | DeviceImportRecord | **Unchanged from Baseline** — already an Independent Component (ADR 0006) | Supporting | Evidenced (Baseline) |
| 10 | Asset and Maintenance | Asset, MaintenanceRecord | New — broader than Device Integration (all physical assets, not just data-producing devices) | Supporting | Evidenced (Wave 5, Cluster D) |
| 11 | Inventory | Stock, Lot | New — distinct lifecycle (receive→store→consume/waste) from Procurement | Supporting | Evidenced (Wave 5, Cluster B) |
| 12 | Procurement | PurchaseRequest, PurchaseOrder | New — distinct approval lifecycle from Inventory | Supporting | Evidenced (Wave 5, Cluster B) |
| 13 | Supplier Management | Supplier evaluation record | New — external-relationship lifecycle, distinct from a single PO | Supporting | Evidenced (Wave 5, Cluster B) |
| 14 | Billing | Invoice, LineItem | **Unchanged from Baseline** (was "Billing and Claims" — Claim now split out, see #16) | Supporting | Evidenced (Baseline) |
| 15 | Payments and Treasury | Payment, Cashbox | New — split from Billing because Treasury/cash-position management is a distinct concern from invoicing | Supporting | Evidenced (Wave 5, Cluster A) |
| 16 | Insurance and Corporate Contracts | Claim, Contract | Split from Baseline's "Billing and Claims" — Claims/Contracts have an external-payer lifecycle distinct from internal Billing | Supporting | Evidenced (Baseline + Wave 5, Cluster H) |
| 17 | Accounting | JournalEntry, Expense | New — general-ledger lifecycle, per Wave 3's Integration-capable recommendation (may lean on external integration more than deep native ownership) | Generic | Evidenced (Wave 5, Cluster A) |
| 18 | Workforce Management | Employee, Shift, Leave, Training | New — HR lifecycle | Generic | Evidenced (Wave 5, Cluster C) |
| 19 | Payroll | PayrollRun | **Split from Workforce Management** per Wave 3's data-sensitivity rationale — own approval/audit chain | Generic (high sensitivity) | Evidenced (Wave 5, Cluster C) |
| 20 | CRM and Support | Lead, SupportCase, Complaint | New — customer-relationship lifecycle | Generic | Evidenced (Wave 5, Cluster E) |
| 21 | Notification and Communication | NotificationRequest | **Unchanged from Baseline** — already an Independent Component | Generic | Evidenced (Baseline) |
| 22 | Document Management | *(controlled documents)* | New — SOP/policy document lifecycle, distinct from clinical Reports (Wave 8 disambiguation) | Generic | Inferred only (Wave 3) |
| 23 | Analytics | *(cross-domain read models)* | New — necessarily reads from every other context; owns no primary data itself | Supporting | Evidenced (Wave 5, Cluster I) |
| 24 | AI Operations | AI Gateway audit trail | **Generalizes Baseline's implicit AI Gateway boundary** into an explicit context, per ADR 0007 | Supporting (governed) | Evidenced (Baseline Phase 10 + Wave 5 Cluster I) |
| 25 | SaaS Commercial Operations | Plan, Subscription, Entitlement | New — commercial/billing lifecycle distinct from clinical Billing (#14) | Commercial | Evidenced (Wave 5, Cluster F) |
| 26 | Tenant and Organization Management | Tenant, Organization, Branch | **Unchanged from Baseline's "Core Platform — Organization and Branch"** | Platform | Evidenced (Baseline) |
| 27 | Identity and Access | User, Role, Permission, Policy | **Unchanged from Baseline's "Core Platform — Identity and Access"** | Platform | Evidenced (Baseline, Constitution Section 10/20) |
| 28 | Audit and Compliance | AuditEvent, ConsentRecord | Split out from the implicit Core Platform grouping — Audit/Consent/Risk/Privacy (Constitution Section 21–23, 30, 58) deserve their own explicit context given their cross-cutting governance weight | Platform | Evidenced (Constitution, Accepted) |

**Not included as a 29th context: "Integration Hub."** The user listed it
as a candidate, but on evidence review, every external integration
discovered so far (Device Integration, Insurance/Payer, future Partner/API)
already has its own ACL pattern owned by its *consuming* context (Device
Integration context itself, Insurance and Corporate Contracts, etc.) — a
separate "Integration Hub" context would either duplicate that ownership or
require re-litigating it. **Recommended: reject as a distinct context**,
keep integration ownership distributed per-consumer as already
established — flagged for the Decision Matrix, not silently dropped.

## Context Mapping — Representative Relationships (not exhaustive 28×28)

| From | To | Pattern | Rationale |
|---|---|---|---|
| Result Verification and Reporting | Laboratory Execution | Customer/Supplier | Verification consumes Processing's output |
| Result Verification and Reporting | Specimen Operations | Customer/Supplier | Unchanged from Baseline |
| Laboratory Execution | Device Integration | Anti-Corruption Layer | Unchanged from Baseline |
| Insurance and Corporate Contracts | Result Verification and Reporting | Open Host Service + Published Language (event-based) | `BillableEventIdentified` trigger, unchanged pattern |
| Billing | Diagnostic Ordering | Customer/Supplier | Unchanged |
| Payments and Treasury | Billing | Partnership *(new pattern in this Wave)* | Both evolve together tightly (an Invoice's lifecycle is incomplete without Payment) — Partnership fits better than Customer/Supplier here, since neither is strictly upstream |
| Payroll | Workforce Management | Customer/Supplier | Payroll consumes Employee/Attendance data but has its own approval chain |
| Analytics | *(every other context)* | Open Host Service + Published Language (read-only) | Analytics never writes to a source context |
| AI Operations | *(every context using AI use cases)* | Open Host Service + Anti-Corruption Layer | Generalizes Baseline Phase 10's Pattern A/B |
| Quality Management | CRM and Support | Customer/Supplier (Complaint → candidate CAPA) | Formalizes the undesigned relationship Wave 4/5 flagged |
| SaaS Commercial Operations | Tenant and Organization Management | Customer/Supplier | Subscription state gates tenant entitlements |
| *(every business context)* | Identity and Access, Audit and Compliance, Tenant and Organization Management | Open Host Service + Published Language | Unchanged Core-Platform pattern from Baseline |

**Shared Kernel:** none adopted (same finding as Baseline Phase 06,
re-confirmed at this larger scale — no pair of contexts was found to need
tighter coupling than Open Host Service/Customer-Supplier provides).

## Decision Matrix — Re-evaluating ADR 0012

| Option | Description | Pros | Cons | Recommendation |
|---|---|---|---|---|
| **Retain as 8** (ADR 0012 unchanged) | Keep the Baseline's Laboratory-scoped map | Simple, matches current evidence depth exactly | Directly contradicts the Confirmed Wave 1 vision (32-domain scope) — indefensible given this program's own findings | **Rejected** |
| **Expand to 28** (this Wave's proposal) | Adopt the full context list above | Matches Confirmed scope; each context has a stated justification; acyclic-graph-compatible (Core Platform contexts remain the universal dependency) | Large surface area, several contexts (17, 18, 20, 22) still only `Inferred`, not `Evidenced` | **Recommended, with explicit caveat below** |
| **Hybrid — 28 named, but only 8 "active"** | Adopt all 28 names now, but formally mark 20 as `Recognized, Not Yet Modeled` (name reserved, no deep tactical work) versus 8 `Modeled` (Baseline-depth) | Avoids implying uniform confidence across all 28; matches actual evidence distribution (Wave 3's finding) honestly | Slightly more complex governance (two context-maturity tiers) | **Also Recommended — arguably the more honest option** |

**Final recommendation for Wave 14 disposition (Recommended, not decided
here):** adopt the **Hybrid** option — supersede ADR 0012 with a new
Proposed ADR naming all 28 contexts but explicitly tiering them by
maturity (Modeled: contexts 1, 4, 5, 6, 7, 9, 21, 26, 27 — the ones with
`Evidenced` status tracing to real Baseline or Wave 5 detail; Recognized:
the remaining 19). This is more defensible than silently treating a
`Document Management` context (0 real evidence) with the same confidence
as `Result Verification and Reporting` (deeply Evidenced).

## Acyclic Graph Check (Platform Contexts Remain the Universal Dependency)

Confirmed: Identity and Access, Audit and Compliance, and Tenant and
Organization Management (contexts 26–28) have zero outgoing dependency
edges in this expanded map, exactly matching the Baseline's Core Platform
rule (Constitution Section 9/10) — every one of the other 25 contexts may
depend on them; they depend on none of the 25. No cycle introduced by the
20 new contexts.
