# API Domain Inventory

Every one of the 28 Modules from the reuse program's Module Catalog
(`docs/reuse/` directory structure, cross-referenced against
`.claude/context/module-catalog.md`) is classified below across the
seven API types this phase requires. This inventory is the canonical
answer to "what kind of API does each Module expose" — `04` through
`14` govern *how*; this document governs *what and to whom*.

## API Type Definitions

| Type | Definition |
|---|---|
| **Internal API** | Contract consumed only by other Modules inside the Modular Monolith. Never Edge-Gateway-routable. |
| **External API** | Exposed via the Edge Gateway to the platform's own authenticated end users (patients, practitioners, staff) through Portals/Dashboards. |
| **Partner API** | Exposed to a specific, contracted third party (a referring clinic, an insurer, a corporate client) under a business relationship — not open registration. |
| **Public API** | Available to any registered third-party developer via self-service. **Deliberately unpopulated below** — the platform has made no Decision to open general-purpose public developer access; that Decision, and its supporting Developer Portal/Marketplace, is explicit Part 2 scope. |
| **Admin API** | Platform/Tenant/Organization/Branch administration — highest-privilege operations (user/role/config management). |
| **Integration API** | Machine-to-machine technical channel with an external system (a device, a clearinghouse, a payment processor) — distinct from Partner API, which is a business relationship; the same counterpart can have both. |
| **Future API** | Explicitly designed-for-later, usually because it is blocked on an unresolved Open Question or reserved for Part 2. |

**Observation (Fact, not a gap):** the Public API column is empty for
every Module. This is a deliberate, honest reflection of current
scope — a general-purpose public developer surface is Part 2 territory
by this phase's own Stop Conditions, not an oversight.

## A. Platform Kernel (3 Modules)

| Module | Internal | External | Partner | Admin | Integration | Future |
|---|---|---|---|---|---|---|
| Identity and Access | Token/session validation contract used by every Module | Login, SSO, self-service profile | — | User/Role/Permission/Policy management | Keycloak Admin REST, wrapped behind ACL | — |
| Tenant and Organization Management | Tenant/Org/Branch resolution contract used by every Module | Org/Branch directory for authenticated users | — | Tenant provisioning, Org/Branch CRUD, feature-flag (Unleash) management | — | Tenant self-service signup (SaaS Commercial Operations dependency) |
| Audit and Compliance | Audit-event emission contract (every Module writes to it) | Caller's own activity/audit view (Data-Scope limited) | — | Compliance/audit query and export | immudb-backed regulator export | — |

## B. Shared Infrastructure / Independent Components (5 Modules)

| Module | Internal | External | Partner | Admin | Integration | Future |
|---|---|---|---|---|---|---|
| Device Integration Gateway | Normalized device-result ingestion contract (ACL output) to Laboratory Execution / Result Verification | — | — | Device registration/monitoring | HL7/ASTM device-facing endpoints (Mirth Connect/Apache Camel) | — |
| Notification Service | Notification-dispatch contract (any Module may request a send) | User notification preferences | — | Template/channel management | Novu-backed multi-channel provider egress (SMS/WhatsApp/email) | — |
| AI Operations Gateway | Governed AI-invocation contract (HITL-enforced per ADR-0007) | — | — | AI policy/model governance | Portkey Gateway-backed LLM provider integration | Patient/practitioner-facing AI-assist API — deferred pending HITL UX design |
| Analytics | Metrics/event ingestion contract | Dashboard/report query (Data-Scope limited) | — | Report/dashboard configuration (Superset-backed) | — | Partner-facing analytics export |
| Document Management | Document storage/retrieval contract | Upload/download/e-signature | — | Retention/workflow policy | Alfresco/Documenso-backed | — |

## C. Core Domain Cluster (7 Modules)

Conditional note: this cluster's REFERENCE+BUILD pattern and its status
as "Core" both depend on ADR-0011 remaining in its current or a
materially similar form (`15-ADR-REVIEW.md`). The API classification
below does not itself resolve that dependency.

| Module | Internal | External | Partner | Admin | Integration | Future |
|---|---|---|---|---|---|---|
| Patient Management | Patient aggregate contract (FHIR-Patient-shaped), consumed by all downstream Core Domain Modules | Patient self-service profile | — | Patient-record administration (Data-Scope gated) | FHIR Patient resource exchange with external referring systems | Cross-tenant patient-matching/MPI API (Open Question-adjacent, not designed) |
| Practitioner and Clinic Management | Practitioner/Clinic directory contract | Practitioner self-service profile | Referring-clinic directory (candidate, not designed) | Credentialing/clinic administration | — | — |
| Scheduling and Encounters | Encounter/Appointment contract | Patient/practitioner-facing booking (Cal.com-backed) | — | Schedule/resource administration | — | Home-collection-logistics booking API — **explicitly blocked on Open Question #6 (Offline Mode / home-collection), not designable yet** |
| Diagnostic Ordering | TestOrder aggregate contract | Practitioner/patient order-status view | Referring-physician order submission (candidate, not designed) | Test-catalog administration (LOINC-backed) | — | — |
| Specimen Operations | Specimen aggregate contract, lifecycle events | Specimen-status view | — | Specimen QC/rejection administration | Barcode/label (ZXing-backed) device interaction | Home-collection-logistics API — same Open Question #6 dependency as Scheduling |
| Laboratory Execution | Analytical-processing contract, Westgard QC events | — | — | Instrument/method configuration | Device Integration Gateway-fed result ingestion | — |
| Result Verification and Reporting | `TestResult` Core Aggregate contract (`ResultVerified`/`ResultReleased` events, HITL-gated) | Patient/practitioner result retrieval (Sensitive Operation) | Referring-clinic result delivery (candidate, not designed) | Verification-authority administration | FHIR DiagnosticReport exchange | **Blocked pending R-06 (FHIR version not pinned)** — not finalizable yet |

## D. Business/Commercial Modules (13 Modules)

| Module | Internal | External | Partner | Admin | Integration | Future |
|---|---|---|---|---|---|---|
| Quality Management | Non-conformance/CAPA event contract | — | — | QM administration (Eramba-backed, conditional risk R-01) | — | — |
| Asset and Maintenance | Asset/maintenance contract | — | — | Asset/maintenance administration (Atlas CMMS-backed, AGPL flag) | — | — |
| Inventory | Stock-ledger contract (single Adoption Point, also serves Asset and Maintenance, Procurement) | — | — | Inventory administration (OpenBoxes-backed) | Supplier/procurement stock sync | — |
| Procurement | Procurement contract | — | Supplier-facing PO/RFQ (candidate, not designed) | Procurement administration (ERPNext-backed) | — | — |
| Supplier Management | Supplier-directory contract | — | Supplier self-service portal (candidate, not designed) | Supplier administration (ERPNext-backed) | — | — |
| Billing | Invoice/charge contract | Patient/practitioner billing self-service | — | Billing administration (ERPNext-backed) | Payment-gateway-abstraction (Omnipay-pattern) egress | — |
| Payments and Treasury | Payment/settlement contract | Patient payment | — | Treasury administration | Fawry/Paymob/WhatsApp-BSP-style vendor integration (wrapped, not independently-adopted SDKs per `05-SDK-BASELINE.md`) | — |
| Insurance and Corporate Contracts | Eligibility/claim contract | Patient coverage-status view | Insurer/corporate-client claims submission (openIMIS-backed, AGPL flag, module-level not whole-app) | Contract administration | `ClaimAdjudicated` external event ingestion (Pivotal Event) | — |
| Accounting | Ledger contract | — | — | Accounting administration (ERPNext-backed) | — | — |
| Workforce Management | Staff/roster contract | Employee self-service | — | Workforce administration (Frappe HR-backed) | — | — |
| Payroll | Payroll contract | Employee payslip self-service | — | Payroll administration (Frappe HR-backed) | — | — |
| CRM and Support | Ticket/contact contract | Customer support-ticket API | — | CRM administration (Frappe Helpdesk/Frappe CRM-backed, AGPL flag, license-drift noted in R-05) | — | — |
| SaaS Commercial Operations | Entitlement/usage-metering contract (Kill Bill + OPA) | Tenant subscription/usage view | Reseller/channel-partner (candidate) | Subscription/plan administration | Kill Bill billing-engine integration | Public developer marketplace/billing surface — **explicitly Part 2** |

## Summary

- **Modules classified: 28/28.**
- **Internal APIs: 28** — every Module has at least one internal
  contract; this is the baseline Modular Monolith expectation.
- **External APIs: 21** — Modules with no direct end-user-facing
  surface (Device Integration Gateway, AI Operations Gateway,
  Laboratory Execution, Quality Management, Asset and Maintenance,
  Inventory, Accounting) are internal/Admin/Integration-only by
  design, not by omission.
- **Partner APIs: 6 candidates identified, 0 designed** — all are
  named as future candidates requiring their own dedicated design pass
  (out of scope for this document, which only inventories, per this
  phase's Do-Not list against designing implementation).
- **Public APIs: 0** — deliberate, Part 2 scope.
- **Future APIs explicitly blocked on an Open Question: 2**
  (home-collection-logistics booking — Scheduling and Encounters,
  Specimen Operations — blocked on Open Question #6; FHIR-shaped
  external exchange — Patient Management, Result Verification and
  Reporting — blocked on `11-RISKS.md` R-06).
