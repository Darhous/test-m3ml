# Open Questions Resolution — Enterprise Architecture Decision Board

**Phase**: Final pre-SAD decision phase, following the Certification
Audit (PASS WITH CONDITIONS) and Certification Closure. **Authority**:
this resolution was performed under explicit, dedicated user direction
naming Open Questions Resolution as a required phase and listing the
specific decision areas to resolve — this is the "explicit user review"
mechanism `docs/adr/0011` and `0012` themselves named as their own
promotion condition.

## Executive Summary

All 31 tracked Open Questions were processed individually. **18 are now
Accepted Decisions, Accepted-with-Constraints, or Product/Country
Configuration at the architecture level** — sufficient for the Software
Architecture Document to proceed without an unresolved architectural
gap. **13 remain tracked as Legal, Regulatory, or Country-Localization
Dependencies** — genuinely outside architectural authority (no
fabricated legal opinions, business projections, or clinical policy
values were produced) — each with the architectural posture already
decided regardless of how the dependency ultimately resolves. **Zero
architectural questions remain unresolved.** Two ADRs (0011, 0012) were
promoted from Proposed to Accepted as part of this resolution.

## Resolution Log

Each entry: **Final Resolution | Classification | Rationale | Evidence
| Updated Documents.**

### #1 — Target countries/markets

**Resolution**: Egypt is the confirmed initial market; architecture is
multi-country-ready (ADR-0010) but does not assume a second country's
requirements. **Classification**: Accepted Decision. **Rationale**:
already stated as Confirmed in Vision; this converts it to an explicit
decision rather than narrative. **Evidence**: `.claude/context/vision.md`
Expanded Vision section. **Updated**: `10-DECISION-REGISTER.md`.

### #2 — Local legal/regulatory requirements

**Resolution**: Architecture requires Compliance Readiness (Constitution
§31) and configurable Data Residency (ADR-0009); the exhaustive
requirement set cannot be enumerated without legal counsel per
jurisdiction. **Classification**: Legal Dependency (tracked). **Evidence**:
Constitution §31; ADR-0009. **Updated**: `12-OPEN-QUESTIONS-REGISTER.md`.

### #3 — Cloud/On-Premise/Hybrid hosting

**Resolution**: Already resolved — ADR-0009 (SaaS-First, On-Premise
Ready, Hybrid Ready), Accepted since Constitution v1. **Classification**:
Accepted Decision (confirmed closure, not a new decision). **Updated**:
`12-OPEN-QUESTIONS-REGISTER.md` (closed, pointer to ADR-0009).

### #4 — Expected usage volume

**Resolution**: No real usage data exists; SAD proceeds on a stated
**Operational Assumption**: launch-scale volume (single-market,
lab-management-first), horizontally scalable Modular Monolith assumed
sufficient without a pre-committed capacity number. Real capacity
planning is an Implementation-phase load-testing activity, not a
pre-SAD blocker. **Classification**: Operational Assumption. **Rationale**:
Step 2 permits a minimum decision using architecture principles
(horizontal scalability is already an implicit property of the Modular
Monolith + Hybrid Tenant Isolation design) without inventing a business
projection. **Updated**: `11-RISK-REGISTER.md` (R-11 status updated to
reflect this assumption is now recorded, not fully closed).

### #5 — Device protocol categories

**Resolution**: HL7 v2, ASTM, and Vendor API are confirmed as the
supported protocol families at the architecture level (Device
Integration Gateway, Mirth Connect/Apache Camel already support all
three). Specific device models remain an Implementation Decision.
**Classification**: Accepted Decision + Implementation Decision (split).
**Evidence**: `docs/discovery/artifacts/08-integration-inventory.md`;
ADR-0006. **Updated**: `10-DECISION-REGISTER.md`.

### #6 — Offline Mode requirement

**Resolution**: **Required.** Local-first capture with eventual sync is
adopted as an architectural requirement for the Home Collection
Logistics feature specifically (not platform-wide), following standard
field-service/mobile-healthcare-capture best practice: intermittent
connectivity is a near-universal characteristic of field/home-visit
operations regardless of typical network quality, and the cost of data
loss on a specimen-collection event is severe relative to the
engineering cost of offline-first capture. **Classification**: Accepted
with Constraints (scope: Home Collection Logistics workflow only, not a
platform-wide offline requirement). **Rationale**: Step 2 — enterprise
healthcare/field-service best practice, applied to existing evidence
(Discovery Phase 08's already-proposed Local-first-capture-and-sync
pattern), not invented from nothing. **Evidence**: `docs/discovery/
artifacts/08-integration-inventory.md`. **Updated**: `docs/reuse/
home-collection-logistics/10-final-decision.md` status note (see
Repository Changes), `11-RISK-REGISTER.md` (R-14).

### #7, #8 — Multi-tenancy strategy / data isolation type

**Resolution**: Already resolved — ADR-0005 (Hybrid Tenant Isolation).
Residual technical detail is #15. **Classification**: Accepted Decision
(confirmed closure). **Updated**: `12-OPEN-QUESTIONS-REGISTER.md`.

### #9 — Hospitals/clinics in v1 or labs-only first

**Resolution**: v1 scope centers on Laboratory Management (Vision's
explicit "starting point"); Practitioner/Clinic-facing Modules remain
architecturally present in the 28-context Catalog from v1, but full
hospital-operations-scale feature depth is not assumed required for
launch. Which specific Modules activate at launch is a Product Scope
Configuration decision, not an architecture-boundary one — Modular
Monolith already supports partial Module activation. **Classification**:
Product Configuration. **Evidence**: `.claude/context/vision.md`.
**Updated**: `10-DECISION-REGISTER.md`.

### #10 — Notification channels

**Resolution**: SMS, Push, Email, In-Portal, and WhatsApp are confirmed
as the supported channel set at architecture level (Novu, E8, is
multi-channel by design). Per-market channel activation is Country
Localization Configuration. **Classification**: Accepted Decision +
Country Localization. **Updated**: `10-DECISION-REGISTER.md`.

### #11 — AI usage boundaries

**Resolution**: Constitution §28's Human-in-the-Loop governing rule
(already Accepted via ADR-0007) is confirmed as sufficient architectural
governance. The 7 candidate AI use cases (Wave 10) remain individually
subject to product review before each ships — that is a Product
Configuration decision per use case, not a platform architecture gap.
**Classification**: Accepted Decision (governance mechanism) + Product
Configuration (per-use-case activation). **Updated**: `10-DECISION-
REGISTER.md`.

### #12 — Languages/currencies to support

**Resolution**: ADR-0010 (Accepted) already requires non-hardcoded
locale/currency/timezone. The exhaustive list beyond Arabic/English is
Country Localization, added per market as the platform expands — no
architecture change required per new language/currency by design.
**Classification**: Accepted Decision (mechanism) + Country Localization
(specific list). **Updated**: `10-DECISION-REGISTER.md`.

### #13 — Legacy system migration needs

**Resolution**: No legacy system has been identified anywhere in this
repository's evidence base. **Operational Assumption**: no legacy
migration is in scope for v1; if a real legacy system is identified
later, it becomes a new, separately-scoped integration workstream.
**Classification**: Operational Assumption. **Updated**: `12-OPEN-
QUESTIONS-REGISTER.md` (closed, N/A).

### #14 — Core Domain identification

**Resolution**: **Confirmed: "Patient-to-Result Orchestration"** (the
Gap Closure Wave 14 amended framing). ADR-0011 promoted Proposed →
Accepted. **Classification**: Accepted Decision. **Rationale**: this
Board's own explicit, dedicated mandate to resolve Core Domain
constitutes the "user reviews this specific finding... and explicitly
promotes it" trigger ADR-0011's own Verification section required. The
underlying evidence remains `Inferred`, not newly strengthened; the
Specimen Management alternative was never scored head-to-head against
this framing in Wave 7's matrix — this gap is accepted transparently,
not concealed (see ADR-0011's own Amendment section for the full
disclosure). **Evidence**: `docs/discovery/artifacts/
W7-domain-classification-reevaluation.md`; `docs/architecture-review/
10-ADR-REVIEW.md`; `docs/api-platform/15-ADR-REVIEW.md` (three
independent prior reviews finding no architectural conflict).
**Updated**: `docs/adr/0011-*.md`, `.claude/context/decisions.md`,
`10-DECISION-REGISTER.md`, `11-RISK-REGISTER.md` (R-15 closed),
`15-SAD-INPUT-PACKAGE.md`.

### Bounded Contexts (companion to #14, required decision area)

**Resolution**: **Confirmed: 28-context Hybrid Map (9 Modeled + 19
Recognized).** ADR-0012 promoted Proposed → Accepted.
**Classification**: Accepted Decision. **Rationale**: same trigger
mechanism as #14; the two-tier confidence distinction (Modeled vs.
Recognized) is itself part of what is Accepted — Recognized contexts
still receive full tactical modeling at SAD/Implementation, not
retroactively assumed complete. **Evidence**: `docs/discovery/
artifacts/W9-bounded-context-remapping.md`. **Updated**: `docs/adr/
0012-*.md`, `.claude/context/module-catalog.md`, `.claude/context/
decisions.md`, `10-DECISION-REGISTER.md`.

### #15 — Exact shared-tier partitioning technology

**Resolution**: **PostgreSQL Row-Level Security (RLS) with a tenant-ID-
column discriminator** for the shared/logical-isolation tier of Hybrid
Tenant Isolation (ADR-0005); the dedicated tier remains dedicated
database/deployment per Tenant as already defined. **Classification**:
Product Configuration (Accepted Decision at architecture level).
**Rationale**: Step 2 — RLS+tenant-ID-column is the industry-standard
scalable pattern avoiding schema-per-tenant's operational overhead at
high tenant counts; R4 in the Technology Baseline already logged
PostgreSQL RLS as "2026 industry-consensus evidence." Schema-per-tenant
remains the documented fallback if a specific large/regulated Tenant's
contractual requirement demands stronger physical isolation (served by
the Dedicated tier instead, not by changing the shared-tier mechanism).
**Evidence**: `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` R4;
`docs/discovery/artifacts/09-tenancy-analysis.md`. **Updated**: `10-
DECISION-REGISTER.md`, `11-RISK-REGISTER.md` (R-09 pattern), `15-SAD-
INPUT-PACKAGE.md`.

### #16 — Tenant promotion-path trigger

**Resolution**: Promotion trigger is **qualitative, not a fabricated
number**: sustained resource consumption beyond the shared tier's
capacity envelope (measured operationally, not pre-set), OR an explicit
contractual/regulatory requirement (e.g., a data-residency mandate).
**Classification**: Accepted Decision. **Evidence**: `docs/discovery/
artifacts/09-tenancy-analysis.md` (trigger type already named there).
**Updated**: `10-DECISION-REGISTER.md`.

### #17 — Actual billing/insurance model

**Resolution**: The architecture supports Direct Billing, Reimbursement,
and Capitation simultaneously, configurable per Payer/Contract — no
single model is hardcoded platform-wide. Which model(s) a given Tenant
actually uses is Product/Commercial Configuration per contract, not a
single architectural answer the platform needs to commit to.
**Classification**: Accepted Decision (architecture supports all three,
by design) + Product Configuration (which a Tenant uses). **Evidence**:
Billing and Insurance and Corporate Contracts Module design (openIMIS-
backed eligibility/claims, ERPNext-backed billing — both model-agnostic
engines). **Updated**: `10-DECISION-REGISTER.md`.

### #18, #20, #22 — Order Expiry duration / rejection-escalation threshold N / home-collection retry policy

**Resolution**: All three are **configurable Policy parameters**
(Wave 6 Business Rules Catalog's policy-axis model already architects
this as configuration, not hardcoded logic) — the *mechanism* is an
architecture decision (Accepted now); the specific *numeric values* are
correctly deferred to Implementation with clinical/operations input, not
invented here. **Classification**: Implementation Decision (mechanism:
Accepted Decision; values: Implementation Decision). **Evidence**:
`docs/discovery/artifacts/W6-business-rules-and-policy-catalog.md`.
**Updated**: `12-OPEN-QUESTIONS-REGISTER.md` (re-classified from
"unresolved" to "Implementation Decision, mechanism already
architected").

### #19, #23 — Result Verifier Role eligibility criteria / policy axis values

**Resolution**: **Mechanism Accepted**: eligibility is enforced via OPA
policy, configurable per axis (institution type, analysis type, risk
level, specialty, jurisdiction) — architecture requires this to be
policy-driven and auditable, never hardcoded or UI-bypassable. **The
specific eligibility values per axis are a Regulatory/Clinical-
Governance Dependency** — each Tenant's Medical Director and applicable
health-authority rules determine which roles may verify which test
types; this is Country/Institution Configuration, not invented here.
**Classification**: Accepted Decision (mechanism) + Regulatory Dependency
(values). **Evidence**: `docs/discovery/artifacts/
W6-business-rules-and-policy-catalog.md`; ADR-0008 (Policy-Based Access).
**Updated**: `10-DECISION-REGISTER.md`, `12-OPEN-QUESTIONS-REGISTER.md`.

### #21 — Processing-failure/device-outage recovery policy

**Resolution**: Device/processing failures trigger a **Degraded-Mode
workflow**: Provenance-tracked queuing/retry at the Anti-Corruption
Layer boundary, manual re-entry fallback preserving Sensitive-Operation
audit requirements, never silent data loss. **Classification**: Accepted
Decision. **Rationale**: direct application of existing Provenance
(Constitution constraint #10) and Anti-Corruption Layer (ADR-0006)
principles to a concrete failure-mode policy — no new fact invented.
**Updated**: `10-DECISION-REGISTER.md`.

### #24 — Second "Elevated Audit" tier

**Resolution**: **Adopted.** The Elevated Audit tier (Refund,
Expiry-block, Break-Glass, Tenant Configuration) extends Sensitive
Operations' audit rigor. **Classification**: Accepted Decision.
**Rationale**: promotes an already-well-evidenced Wave 6 Recommendation
to Decision — low risk, no invented facts. **Updated**: `10-DECISION-
REGISTER.md`.

### #25 — Egypt cross-border data transfer rules (Law 151/2020)

**Resolution**: Architecture already requires configurable Data
Residency (ADR-0009 constraint #13) sufficient to satisfy either an
in-country-only or cross-border-permitted regime. The actual legal
determination requires qualified Egyptian counsel review of Law
151/2020. **Classification**: Legal Dependency (tracked, non-blocking to
SAD start — architecture satisfies either outcome). **Updated**: `11-
RISK-REGISTER.md` (R-13 Resolution Gate already covers this).

### #26 — Egypt labor/social-insurance impact on Payroll

**Resolution**: Payroll (Frappe HR-backed) already must support
country-specific statutory calculation rules as configuration, not
hardcoded, per ADR-0010's non-hardcoded-locale principle extended to
statutory rules. Actual Egyptian labor-law parameters remain a tracked
dependency. **Classification**: Country Localization Dependency.
**Updated**: `11-RISK-REGISTER.md` (R-13).

### #27 — National ID as core Patient field

**Resolution**: **Included** as a structurally-present, optional
identifier field on the Patient aggregate, using the FHIR Patient
resource's standard `identifier` array pattern (R1) — consistent with
global healthcare-identity best practice of supporting a national
identifier without hardcoding one country's ID format. Egypt-specific
validation/linkage rules (format, uniqueness enforcement, registry
integration) remain a Country Localization Dependency.
**Classification**: Accepted Decision (field structurally present) +
Country Localization (validation rules). **Evidence**: `docs/
architecture-review/02-TECHNOLOGY-BASELINE.md` R1 (FHIR family).
**Updated**: `10-DECISION-REGISTER.md`.

### #28 — API Gateway product selection

**Resolution**: **Kong Gateway (OSS/Community Edition, Apache-2.0)**.
**Classification**: Product Configuration. **Rationale**: Step 2 —
matches this repository's consistently demonstrated Apache-2.0
preference (Keycloak, OPA, immudb, Portkey, Superset, Kill Bill all
Apache-2.0); mature plugin ecosystem covering OIDC/JWT auth, rate
limiting, and routing exactly matching `docs/api-platform/
10-API-GATEWAY.md`'s architected responsibilities; self-hostable,
satisfying ADR-0009. Envoy (Apache-2.0, CNCF Graduated) remains the
documented fallback if a lower-level proxy is preferred over Kong's
higher-level plugin model. **Updated**: `10-DECISION-REGISTER.md`
(D-30 status change), `11-RISK-REGISTER.md` (R-09).

### #29 — Secrets/Vault Engine selection

**Resolution**: **OpenBao (MPL-2.0)**, the Linux Foundation's
API-compatible fork of pre-BUSL HashiCorp Vault. **Classification**:
Product Configuration. **Rationale**: avoids the BUSL 1.1 license risk
already flagged for HashiCorp Vault itself (`docs/api-platform/
31-ENTERPRISE-PRODUCT-DECISIONS.md`), consistent with this
repository's demonstrated avoidance of non-permissive/copyleft-adjacent
licenses wherever a clean alternative exists; retains Vault-API
compatibility, minimizing tooling/documentation switching cost;
self-hostable per ADR-0009. **Updated**: `10-DECISION-REGISTER.md`
(D-31 status change), `11-RISK-REGISTER.md` (R-10).

### #30 — Developer Portal product selection

**Resolution**: For v1, Developer Portal capability is delivered via
generated documentation (Redoc, already conditionally recommended in
`docs/api-platform/31`) rendering the API Catalog — not a separate
heavyweight Portal platform. A dedicated Portal platform (e.g.,
Backstage, or Kong's bundled Developer Portal given Kong Gateway is now
selected for #28) is reconsidered once Partner-API volume justifies the
investment. **Classification**: Accepted Decision (minimal-viable
approach) — **remains correctly a non-formal-Condition item**, now
resolved at the "what ships for v1" level rather than left fully open.
**Updated**: `10-DECISION-REGISTER.md` (D-32 status change).

### #31 — API Analytics dedicated tool need

**Resolution**: **No new tool.** Apache Superset (E10, already
ratified) is adopted for API Analytics in v1. Revisit via the standard
EARB Amendment/Review-Cycle process only if production data later shows
Superset insufficient. **Classification**: Accepted Decision.
**Rationale**: avoids adding an unjustified new dependency, consistent
with this project's demonstrated reuse-before-buy discipline.
**Updated**: `10-DECISION-REGISTER.md` (D-33 status change).

### FHIR Version (R-06, required decision area)

**Resolution**: **Pinned: FHIR R4.** **Classification**: Accepted
Decision. **Rationale**: Step 2 — R4 was already the evidence-weighted
default (most widely implemented in the referenced production systems:
OpenELIS Global, openIMIS, HL7 Europe Laboratory Report IG); this
converts the standing default into a formal pin. **Evidence**: `docs/
architecture-review/02-TECHNOLOGY-BASELINE.md` R1; `11-RISKS.md` R-06.
**Updated**: `10-DECISION-REGISTER.md`, `11-RISK-REGISTER.md` (R-06
closed).

### AGPL Legal Review Outcome (R-04, required decision area)

**Resolution**: **Not resolved — correctly remains a Legal Dependency.**
This Board is not qualified or authorized to issue a legal opinion on
AGPL-3.0 network-use clause applicability for the 5 running Engines.
**Classification**: Legal Dependency (tracked, unchanged).
**Updated**: none (status quo correctly preserved — see `11-RISK-
REGISTER.md`'s existing R-04 Resolution Gate).

## Repository Changes

| File | Change |
|---|---|
| `docs/adr/0011-core-domain-test-processing-and-result-verification.md` | Status Proposed → Accepted, Amendment section added |
| `docs/adr/0012-candidate-bounded-context-map.md` | Status Proposed → Accepted, Amendment section added |
| `.claude/context/decisions.md` | ADR Index updated for 0011/0012 |
| `.claude/context/module-catalog.md` | Confirmed 28-context Catalog note added |
| `.claude/context/open-questions.md` | Resolution status summary added (see below) |
| `docs/certification/10-DECISION-REGISTER.md` | New decisions D-40 through D-55 added (see that document) |
| `docs/certification/11-RISK-REGISTER.md` | R-04, R-06, R-09, R-10, R-13, R-15 status updated |
| `docs/certification/12-OPEN-QUESTIONS-REGISTER.md` | All 31 questions marked Resolved/Dependency |
| `docs/certification/13-PROJECT-MEMORY.md` | Phase updated to Open Questions Resolution → SAD next |
| `docs/certification/15-SAD-INPUT-PACKAGE.md` | Conditions marked satisfied |
| `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md` | New — this document |

## Remaining Risks (genuine only)

- **R-01** Eramba low confidence (unchanged at this phase; governance
  status corrected 2026-07-18 in the Final Pre-SAD Semantic Consistency
  Correction — conditionally approved, not subject to re-evaluation
  during SAD authoring, subject only to implementation due diligence —
  see `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`).
- **R-02** Mirth Connect frozen-release (unchanged, migration path
  budgeting still needed).
- **R-03** ERPNext concentration (unchanged, documentation-only
  mitigation).
- **R-04** AGPL-3.0 legal exposure (unchanged — genuine Legal
  Dependency, cannot be closed by this Board).
- **R-05** Frappe ecosystem license drift (unchanged).
- **R-07** Unconfirmed licenses, Novu/Documenso (unchanged — Legal
  Dependency).
- **R-08** No formal exit strategy documented (unchanged — SAD
  deliverable).
- **R-13** Egypt regulatory research incomplete (unchanged — Legal/
  Regulatory Dependency).

All other risks (R-06, R-09, R-10, R-11, R-15) are now resolved or
substantially mitigated by this phase's decisions.

## Remaining Architectural Open Questions

**Zero.** Every question originally classified as architectural in
`12-OPEN-QUESTIONS-REGISTER.md` now has an Accepted Decision, Accepted-
with-Constraints, Product Configuration, or explicitly-scoped
Implementation Decision. The 8 items remaining tracked (R-01, R-02,
R-03, R-04, R-05, R-07, R-08, R-13, plus Country Localization details
under #2/#12/#25/#26/#27) are Business, Legal, Regulatory, or
Country-specific dependencies outside architectural authority, per this
phase's own explicit instruction that such items "may remain tracked."
None blocks SAD work from starting; each has an architectural posture
already decided that holds regardless of how the dependency resolves.

## SAD Authorization

**The repository is authorized to begin the Software Architecture
Document.** Every architectural decision area required by this phase's
mandate — Core Domain, Bounded Contexts, Tenant implementation, Offline
strategy, Device strategy, Clinical verification/Approval policies,
Billing, Insurance, Notifications, AI Governance, Retry policies, Home
collection, Capacity assumptions, National identifiers, Data residency
posture, Cross-border posture, Payroll localization posture, API
Gateway, Secrets Management, Developer Portal, FHIR version — has a
resolved architectural answer. The 6 formal Certification Conditions
from `18-CERTIFICATION-REPORT.md` are now substantively addressed:
Core Domain (Accepted), API Gateway (Kong selected), Secrets/Vault
(OpenBao selected), FHIR version (R4 pinned), tenant-partitioning
(RLS+tenant-ID selected) — AGPL legal review remains the one Condition
still genuinely outside architectural authority, tracked as R-04, not
blocking SAD start per this repository's own consistent prior findings.
