# Technology Baseline (FROZEN)

**Status: FROZEN as of this review.** This is the mandatory technology
reference for API Platform Strategy, the SAD, Core Platform, SDK, and
Module development. A row changes only through a new ADR or a
subsequent EARB review cycle — never by silent edit (same discipline as
`MASTER_DECISION_REGISTER.md`'s append-only rule).

**Field definitions:** *Approved Version* is the version confirmed
active in `MASTER_REPOSITORY_DATABASE.md`'s "Latest Activity" column
where recorded, else "Latest stable at implementation time" (the reuse
program did not pin every version). *Owner* is the Bounded Context/
Module that holds the Single Adoption Point per `MASTER_DEPENDENCY_
MATRIX.md` — the team responsible for the integration, not necessarily
every consuming Module. *Review Cycle* follows Constitution Section 55's
Evolution Strategy discipline: Annual for stable/low-risk adoptions,
Semi-Annual for AGPL/tentative/frozen-release adoptions.

## A. Engines (21)

| # | Technology | Category | Decision | Approved Version | License | Upgrade Policy | Replacement Candidate | Risk | Owner (Single Adoption Point) | Review Cycle | ADR Reference |
|---|---|---|---|---|---|---|---|---|---|---|---|
| E1 | Keycloak | Identity Engine | APPROVED | 26.5.7 (Apr 2026) or later stable | Apache-2.0 | Track upstream minor releases; security patches within 1 sprint | Zitadel (AGPL, not preferred), Authentik | Low | Identity and Access | Annual | ADR-0008 |
| E2 | Open Policy Agent (OPA) | Policy Engine | APPROVED | Latest stable, CNCF Graduated | Apache-2.0 | Track upstream; policy bundles versioned independently | Casbin | Low | Identity and Access (`authorization-rbac-abac`) | Annual | ADR-0008 |
| E3 | Unleash | Feature Flag / Config Engine | APPROVED | OSS edition, latest stable | Apache-2.0 | Track upstream | Flagsmith (BSD-3, not preferred — avoids 2nd flag engine) | Low | Tenant and Organization Management | Annual | — |
| E4 | immudb | Immutable Audit Store | APPROVED | 1.11 (May 2026) or later | Apache-2.0 | Track upstream | Trillian | Low | Audit and Compliance | Annual | — |
| E5 | Eramba Community | Compliance/GRC Engine | **CONDITIONALLY APPROVED — reconsider at SAD** | Latest stable | GPL-3.0 (unverified this pass) | Hold; do not deepen integration until reconsidered | CISO Assistant, GovReady-Q | **Medium — lowest-confidence decision in the program** | Audit and Compliance | Semi-Annual | — |
| E6 | Mirth Connect | HL7/ASTM Integration Engine | APPROVED (conditional) | 4.5.2 — **frozen, last free release** | MPL-2.0 (4.5.2 only; 4.6+ commercial) | **No free security patches past 4.5.2** — treat as a frozen dependency, not an upgradeable one | Apache Camel (Apache-2.0, active) | **High — frozen-release risk** | Device Integration Gateway | Semi-Annual | ADR-0006 |
| E7 | RabbitMQ | Message Broker | APPROVED | Latest stable | MPL-2.0 | Track upstream | Apache Kafka, NATS JetStream | Low | Device Integration Gateway (platform-wide) | Annual | ADR-0004 |
| E8 | Novu | Multi-Channel Notification Engine | APPROVED | Latest stable | **Unconfirmed — `Requires Legal Verification`** | Hold major-version upgrades pending license reconfirmation | Courier, Knock (both SaaS-first, not preferred) | Medium — license unconfirmed | Notification Service (platform-wide) | Semi-Annual | ADR-0007 (adjacent) |
| E9 | Portkey Gateway | LLM Gateway | APPROVED | Latest stable (full OSS since March 2026) | Apache-2.0 | Track upstream; re-verify OSS status annually given recency of the license change | LiteLLM | Low-Medium — recent license change, re-verify | AI Operations Gateway | Annual | ADR-0007 |
| E10 | Apache Superset | BI/Analytics Engine | APPROVED | Latest stable | Apache-2.0 | Track upstream | Metabase (AGPL, paywalled white-label — not preferred), Lightdash | Low | Analytics | Annual | — |
| E11 | Alfresco Community Edition | Document/Workflow Engine | APPROVED | Latest Community stable | LGPL-3.0 (unverified this pass) | Track upstream; reconfirm license at implementation | Nextcloud Hub (AGPL, not preferred) | Medium — license unverified | Document Management | Semi-Annual | — |
| E12 | Documenso | E-Signature Engine | APPROVED | Latest stable | **Unconfirmed — `Requires Legal Verification`** | Hold pending license reconfirmation | OpenSign (AGPL, credible fallback) | Medium — license unconfirmed, Sensitive-Operation-adjacent | Document Management | Semi-Annual | — |
| E13 | Cal.com | Patient Scheduling Engine | APPROVED | Core, latest stable | AGPL-3.0 (core) | Hold pending legal review; commercial license is a documented escape hatch | Cal.diy (MIT fork, credible fallback) | Medium — AGPL, `Requires Legal Verification` | Scheduling and Encounters | Semi-Annual | — |
| E14 | Atlas CMMS | Asset/Maintenance Engine | APPROVED | Latest stable | AGPL-3.0 (dual, commercial available) | Hold pending legal review; commercial license is a documented escape hatch | openMAINT | Medium — AGPL, `Requires Legal Verification` | Asset and Maintenance | Semi-Annual | — |
| E15 | OpenBoxes | Inventory/Supply Chain Engine | APPROVED | Latest stable | Eclipse Public License 1.0 | Track upstream | Odoo Inventory (LGPL-3.0), ERPNext Stock (explicitly not used — see `06-FORK-BASELINE.md` duplicate-avoidance note) | Low — cleanest license of any Engine in the program | Inventory (single stock-ledger Adoption Point, also serves Asset and Maintenance, Procurement) | Annual | — |
| E16 | ERPNext | ERP / Financial Backbone | APPROVED | Latest stable | GPL-3.0 | Track upstream; clear for self-hosted use | Odoo (open-core risk, not preferred) | Low-Medium — broadest single-Engine footprint (5 Modules), concentration risk | Procurement (single Adoption Point, also serves Supplier Management, Billing, Payments and Treasury, Accounting) | Annual | — |
| E17 | openIMIS | Health Insurance/Claims Engine | APPROVED | Latest stable | AGPL-3.0 | Hold pending legal review; module-level (not whole-app) adoption | N/A — no comparable Digital Public Good alternative found | Medium — AGPL, `Requires Legal Verification` | Insurance and Corporate Contracts | Semi-Annual | — |
| E18 | Frappe HR | HR/Payroll Engine | APPROVED | Latest stable | GPL-3.0 | Track upstream alongside ERPNext | N/A — same-vendor-family, no evaluated alternative | Low | Workforce Management (also serves Payroll) | Annual | — |
| E19 | Frappe Helpdesk | Support/Ticketing Engine | APPROVED | Latest stable | AGPL-3.0 | Hold pending legal review — **license-drift from Frappe HR/ERPNext, do not assume inherited clearance** | Zammad, osTicket (not evaluated this pass) | Medium — AGPL, `Requires Legal Verification` | CRM and Support | Semi-Annual | — |
| E20 | Frappe CRM | Sales/Contact CRM Engine | APPROVED | Latest stable | AGPL-3.0 | Hold pending legal review — same license-drift caveat as E19 | Not evaluated this pass | Medium — AGPL, `Requires Legal Verification` | CRM and Support | Semi-Annual | — |
| E21 | Kill Bill | Subscription/SaaS Billing Engine | APPROVED | Latest stable | Apache-2.0 | Track upstream | Lago (AGPL, credible modern fallback) | Low — clean license, 10+ years enterprise-proven | SaaS Commercial Operations | Annual | — |

## B. Libraries (4)

| # | Technology | Category | Decision | Approved Version | License | Upgrade Policy | Replacement Candidate | Risk | Owner | Review Cycle | ADR Reference |
|---|---|---|---|---|---|---|---|---|---|---|---|
| L1 | pgvector | PostgreSQL extension (vector search) | APPROVED | Latest stable | PostgreSQL License | Track upstream with PostgreSQL itself | Qdrant, Weaviate (dedicated vector DB, only if scale triggers it) | Low | AI Operations Gateway | Annual | — |
| L2 | Prophet | Statistical forecasting library | APPROVED | Latest stable | MIT | Track upstream | N/A | Low | Analytics | Annual | — |
| L3 | FullCalendar | Calendar-rendering UI component | APPROVED | Core, latest stable | MIT (core; premium plugins separately licensed) | Track upstream; avoid premium plugins unless separately licensed | N/A | Low | Scheduling and Encounters | Annual | — |
| L4 | ZXing (or equivalent) | Barcode encode/decode library | APPROVED (general-knowledge basis) | Latest stable | Apache-2.0 | **Re-confirm specific library and license at implementation time** — this program disclosed it did not freshly re-search this candidate | Any maintained barcode library equivalent | Low-Medium — general-knowledge basis, not freshly verified | Specimen Operations (also serves Inventory) | Annual (re-verify at implementation first) | — |

## C. Reference Standards / Patterns (5)

Not licensed software dependencies in the conventional sense — these are
data-model, protocol, or architecture patterns adopted by reference, per
`MASTER_REUSE_MATRIX.md`. Included here because they are formally
"adopted technology decisions" the SAD must treat as fixed inputs.

| # | Standard | Category | Decision | Version/Edition | License | Upgrade Policy | Replacement Candidate | Risk | Owner | Review Cycle | ADR Reference |
|---|---|---|---|---|---|---|---|---|---|---|---|
| R1 | HL7 FHIR Resource Family (Patient, Practitioner, ServiceRequest/Task, Encounter, Specimen, DiagnosticReport, Claim, Coverage, EligibilityRequest/Response) | Clinical Data Model Standard | APPROVED | FHIR R4 (assumed — **not explicitly version-pinned by the reuse program, flagged below**) | HL7 FHIR License | Track HL7 releases | N/A — industry standard | Low — but see `11-RISKS.md` R-06 (version not pinned) | Patient Management (originating Adoption Point, reused across 7 Modules) | Annual | ADR-0011 (Core Domain, Proposed-Amended — see `10-ADR-REVIEW.md`) |
| R2 | LOINC | Diagnostic Test Coding Standard | APPROVED | Latest release | Regenstrief free-use license | Track Regenstrief releases | N/A | Low | Diagnostic Ordering | Annual | — |
| R3 | Westgard Rules | Statistical QC Methodology | APPROVED | N/A — public methodology | Public, not licensed software | N/A | N/A | Low | Laboratory Execution | N/A | — |
| R4 | PostgreSQL Row-Level Security | Multi-Tenancy Data-Isolation Pattern | APPROVED (Reference, not a resolution) | N/A — database-native feature | PostgreSQL License | Tied to PostgreSQL's own release cycle | Schema-per-tenant (the SAD's still-open alternative) | Medium — feeds but does not resolve Open Question #15 | Tenant and Organization Management | N/A until `open-questions.md` #15 resolved | ADR-0005 |
| R5 | Omnipay adapter-pattern architecture | Payment Gateway Abstraction Pattern | APPROVED (architecture Reference only) | N/A — not a code dependency | MIT (informational only) | N/A | N/A | Low | Payments and Treasury | N/A | — |

## Summary Counts

- **Engines ratified: 21** (19 fully Approved, 2 Conditionally Approved
  — Eramba, and Mirth Connect's frozen-release status carried forward
  as a standing High risk, not a rejection)
- **Libraries ratified: 4**
- **Reference Standards ratified: 5**
- **Total Technology Baseline entries: 30**
- **SDKs ratified: 0** (see `05-SDK-BASELINE.md`)
- **Controlled Forks ratified: 0** (see `06-FORK-BASELINE.md`)
