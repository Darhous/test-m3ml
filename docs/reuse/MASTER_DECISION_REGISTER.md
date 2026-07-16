# Master Decision Register

The single authoritative log of every Build-vs-Buy decision made in this
program, in decision order (append-only, one row per Feature, never
edited after the fact — a changed decision gets a new row with a
"Supersedes" note, matching the Discovery program's own change-control
discipline). This is the audit trail; `MASTER_BUILD_VS_BUY_MATRIX.md` is
the current-state index.

| # | Date | Module | Feature | Decision | Rationale (one line) | Supersedes |
|---|---|---|---|---|---|---|
| 1 | 2026-07-16 | Identity and Access | authentication | ENGINE + ADAPTER: Keycloak | Highest weighted score, cleanest license, explicit regulated-industry adoption evidence | — |
| 2 | 2026-07-16 | Identity and Access | sso-oidc-oauth | ENGINE + ADAPTER: Keycloak (same Engine) | Cross-Feature Dependency — same repo | — |
| 3 | 2026-07-16 | Identity and Access | multi-factor-auth | ENGINE + ADAPTER: Keycloak (same Engine) | Cross-Feature Dependency — same repo | — |
| 4 | 2026-07-16 | Identity and Access | session-management | ENGINE + ADAPTER: Keycloak (same Engine) | Cross-Feature Dependency — same repo | — |
| 5 | 2026-07-16 | Identity and Access | user-group-management | ENGINE + ADAPTER: Keycloak (same Engine) | Cross-Feature Dependency — same repo | — |
| 6 | 2026-07-16 | Identity and Access | authorization-rbac-abac | ENGINE + ADAPTER (dual): Keycloak RBAC + OPA ABAC | 8-dimension Policy Model exceeds general-purpose IAM RBAC; OPA is CNCF Graduated and purpose-built | — |
| 7 | 2026-07-16 | Identity and Access | audit-hooks-integration | LIBRARY: thin adapter over Keycloak Event Listener SPI | Integration glue, not an independent Engine decision | — |
| 8 | 2026-07-16 | Tenant and Organization Management | tenant-provisioning | BUILD: orchestration Saga over Keycloak + PostgreSQL | Platform-specific workflow, no product fits | — |
| 9 | 2026-07-16 | Tenant and Organization Management | organization-branch-hierarchy | BUILD: platform-owned business-data schema | Core domain modeling, not infrastructure | — |
| 10 | 2026-07-16 | Tenant and Organization Management | multi-tenancy-isolation | REFERENCE: PostgreSQL Row-Level Security pattern | Industry-consensus default; database-native, no product to adopt; evidence for `open-questions.md` #15, not a resolution | — |
| 11 | 2026-07-16 | Tenant and Organization Management | feature-flags | ENGINE + ADAPTER: Unleash via OpenFeature | Governance/audit features fit Sensitive-Operation-adjacent gating; regulated-sector adoption evidence | — |
| 12 | 2026-07-16 | Tenant and Organization Management | tenant-configuration | ENGINE + ADAPTER (shared Unleash) + BUILD (complex config) | Avoids a second flag/config engine (Flagsmith rejected for this reason specifically) | — |
| 13 | 2026-07-16 | Audit and Compliance | immutable-audit-trail | ENGINE + ADAPTER: immudb | Cryptographic tamper-evidence, holds even against a malicious DBA; explicit 2026 healthcare framing | — |
| 14 | 2026-07-16 | Audit and Compliance | consent-management | REFERENCE (FHIR Consent) + BUILD (enforcement via OPA) | No dedicated clinical-consent engine exists; Klaro-class tools are website/cookie consent, a real category mismatch, not force-fit | — |
| 15 | 2026-07-16 | Audit and Compliance | policy-engine | ENGINE + ADAPTER (shared OPA) | Same engine as Identity and Access `authorization-rbac-abac`, 2nd consuming Module | — |
| 16 | 2026-07-16 | Audit and Compliance | compliance-tracking | ENGINE + ADAPTER: Eramba Community (tentative, low confidence) | Weakest-evidence decision in the program so far; explicitly flagged for SAD-level reconsideration | — |
| 17 | 2026-07-16 | Audit and Compliance | document-control | CONSOLIDATED — deferred to Document Management | Detected duplicate of Document Management's `document-control-workflow`; avoids duplicate research | — |
| 18 | 2026-07-16 | Device Integration Gateway | hl7-integration-engine | ENGINE + ADAPTER (tentative): Mirth 4.5.2, Camel fallback | Best healthcare-purpose fit, but frozen since NextGen's March 2025 licensing change — explicitly flagged | — |
| 19 | 2026-07-16 | Device Integration Gateway | astm-integration | ENGINE + ADAPTER (shared) + BUILD | Follows hl7-integration-engine; weak native ASTM tooling on both candidates | — |
| 20 | 2026-07-16 | Device Integration Gateway | device-protocol-adapters | BUILD | No product exists per-vendor by definition | — |
| 21 | 2026-07-16 | Device Integration Gateway | message-broker-queueing | ENGINE + ADAPTER: RabbitMQ | Durable, moderate-scale fit; resolves 2 prior Modules' deferred delivery-guarantee questions | — |
| 22 | 2026-07-16 | Notification Service | multi-channel-notification-engine | ENGINE + ADAPTER: Novu (license TBC) | Only credible self-hostable OSS multi-channel engine found; Courier/Knock/SuprSend are SaaS-first | — |
| 23 | 2026-07-16 | Notification Service | templating | ENGINE + ADAPTER (shared Novu) | Built-in per-channel template editor | — |
| 24 | 2026-07-16 | Notification Service | delivery-tracking | ENGINE + ADAPTER (shared Novu) | Built-in delivery-status tracking | — |
| 25 | 2026-07-16 | Notification Service | whatsapp-integration | ENGINE + ADAPTER (shared Novu) + SDK (BSP, vendor TBD) | Native WhatsApp provider; BSP is a commercial decision, not software Build-vs-Buy | — |
| 26 | 2026-07-16 | AI Operations Gateway | llm-gateway-orchestration | ENGINE + ADAPTER: Portkey | March-2026 full-OSS release with native guardrails matching Constitution Section 28; LiteLLM credible fallback | — |
| 27 | 2026-07-16 | AI Operations Gateway | prompt-audit-logging | ENGINE + ADAPTER (composed: Portkey + immudb) | Reuses Module 3's immutable store | — |
| 28 | 2026-07-16 | AI Operations Gateway | ai-use-case-governance | ENGINE + ADAPTER (composed: Portkey + OPA) | OPA's 4th confirmed reuse across 3 Modules | — |
| 29 | 2026-07-16 | AI Operations Gateway | semantic-search | REFERENCE/LIBRARY: pgvector | Reuses existing PostgreSQL; no measured need for a dedicated vector DB | — |
| 30 | 2026-07-16 | Analytics | bi-dashboards | ENGINE + ADAPTER: Apache Superset | Decisive White-Label fit (Confirmed Wave 1); Metabase's OSS tier paywalls embedding | — |
| 31 | 2026-07-16 | Analytics | embedded-analytics | ENGINE + ADAPTER (shared Superset) | Embedding SDK was the decisive factor for bi-dashboards | — |
| 32 | 2026-07-16 | Analytics | reporting-engine | ENGINE + ADAPTER (composed: Superset + Novu) | Native Alerts & Reports feature, delivered via already-selected Notification Service | — |
| 33 | 2026-07-16 | Analytics | forecasting-engine | LIBRARY: Prophet | Robust starting choice for moderate/messy data; lower priority per Wave 3/10's speculative classification | — |
| 34 | 2026-07-16 | Document Management | document-storage-versioning | ENGINE + ADAPTER: Alfresco Community (license TBC) | Built-in Activiti workflow engine solves 2 Features at once | — |
| 35 | 2026-07-16 | Document Management | document-control-workflow | ENGINE + ADAPTER (shared Alfresco) | **Resolves Module 3's deferred `document-control` duplicate** | Supersedes deferred Decision (Module 3, row 17) |
| 36 | 2026-07-16 | Document Management | e-signature | ENGINE + ADAPTER: Documenso (license TBC) | SOC 2 compliance work + funded backing outweigh OpenSign's zero cost for a Sensitive-Operation-adjacent Feature | — |
| 37 | 2026-07-16 | Patient Management | patient-registry-mpi | REFERENCE (FHIR Patient) + BUILD | **OpenMRS explicitly evaluated and rejected** as a whole-system adoption -- would displace ADR-0011's Amended Core Domain; OpenCR logged as the future MPI upgrade path | — |
| 38 | 2026-07-16 | Patient Management | patient-history-timeline | BUILD | Core-Domain-adjacent read-model, no product category exists | — |
| 39 | 2026-07-16 | Patient Management | patient-portal-ui | BUILD | White-Label branding rules out a generic portal product | — |
| 40 | 2026-07-16 | Patient Management | consent-linkage | REFERENCE + BUILD (shared Module 3) | Reference-only linkage to the already-selected Consent Aggregate | — |
| 41 | 2026-07-16 | Practitioner and Clinic Management | practitioner-registry-credentialing | REFERENCE (FHIR Practitioner) + BUILD | Same Core-Domain-preservation rationale as Patient Management | — |
| 42 | 2026-07-16 | Practitioner and Clinic Management | clinic-facility-directory | BUILD | Join structure over 2 already-modeled Aggregates | — |
| 43 | 2026-07-16 | Practitioner and Clinic Management | referral-management | REFERENCE (FHIR ServiceRequest) + BUILD | Platform-owned workflow, FHIR-shaped data model | — |
| 44 | 2026-07-16 | Scheduling and Encounters | appointment-scheduling-engine | ENGINE + ADAPTER: Cal.com (license TBC) | Explicit, current healthcare scheduling use cases (SOC 2, HIPAA-friendly); Cal.diy MIT fork as fallback | — |
| 45 | 2026-07-16 | Scheduling and Encounters | resource-calendar | LIBRARY: FullCalendar | Decade-mature calendar-rendering library, distinct category from booking logic | — |
| 46 | 2026-07-16 | Scheduling and Encounters | encounter-tracking | REFERENCE (FHIR Encounter) + BUILD | Core-Domain-preserving, same pattern as Modules 9-10 | — |
| 47 | 2026-07-16 | Scheduling and Encounters | reminders-integration | ENGINE + ADAPTER (shared Novu) | Avoids a 2nd notification engine specific to scheduling | — |
| 48 | 2026-07-16 | Diagnostic Ordering | order-entry-cpoe | REFERENCE (FHIR ServiceRequest/Task) + BUILD | Cross-validated by 2 independent production LIS/EMR ecosystems (OpenELIS, Bahmni); OpenELIS/Bahmni themselves not adopted wholesale | — |
| 49 | 2026-07-16 | Diagnostic Ordering | order-catalog-pricing | REFERENCE (LOINC) + BUILD | Tenant-specific pricing correctly platform-owned; LOINC gives standardized naming for free | — |
| 50 | 2026-07-16 | Diagnostic Ordering | order-status-tracking | REFERENCE (FHIR Task) + BUILD (shared) | Read-model over the same Task-state pattern | — |
| 51 | 2026-07-16 | Specimen Operations | specimen-accessioning | REFERENCE (FHIR Specimen) + BUILD | Same Core-Domain-preservation pattern as Modules 9-12; whole-system SENAITE/OpenELIS question deliberately deferred to Module 14 | — |
| 52 | 2026-07-16 | Specimen Operations | barcode-labeling | LIBRARY: ZXing (or equivalent) | Mature, standard barcode-decoding library category; disclosed as general-knowledge-based, not freshly searched this pass | — |
| 53 | 2026-07-16 | Specimen Operations | chain-of-custody | BUILD (event-chain feeding immudb) | Platform-specific custody-event workflow, no product fits; reuses Module 3's tamper-evident store | — |
| 54 | 2026-07-16 | Specimen Operations | home-collection-logistics | **DEFERRED — blocked on `open-questions.md` #6** | Cannot honestly classify until Offline Mode requirement is resolved; No-Guessing Rule applies | — |
| 55 | 2026-07-16 | Laboratory Execution | worklist-management | REFERENCE (OpenELIS Global primary, SENAITE secondary) + BUILD | Resolves Modules 12-13's twice-deferred decision; wholesale ENGINE+ADAPTER adoption of either mature LIMS genuinely weighed and rejected — displaces ADR-0011 Amended Core Domain at its most central point | — |
| 56 | 2026-07-16 | Laboratory Execution | analyzer-middleware-integration | ENGINE + ADAPTER (shared Mirth/Camel, Module 4) + BUILD | Cross-Feature Dependency — same HL7/ASTM engine as Module 4, not re-decided | — |
| 57 | 2026-07-16 | Laboratory Execution | quality-control-tracking | REFERENCE (Westgard rules + SENAITE module design) + BUILD | No standalone product exists; Westgard rules are public methodology; whole-LIMS candidates already rejected | — |
| 58 | 2026-07-16 | Laboratory Execution | calibration-tracking | BUILD | Join structure over Analyzer + QC run-recording, no product fits | — |
| 59 | 2026-07-16 | Result Verification and Reporting | result-review-verification-workflow | ENGINE + ADAPTER (shared OPA) + BUILD | 5th confirmed OPA reuse; the 8-dimension Policy Model authorization decision was already made at Module 1, this is its Core Domain workflow application | — |
| 60 | 2026-07-16 | Result Verification and Reporting | clinical-report-generation | LIBRARY (candidate deferred) + BUILD | No dedicated clinical-report-renderer product found; specific PDF/templating library correctly deferred to implementation time (stack-dependent), not guessed | — |
| 61 | 2026-07-16 | Result Verification and Reporting | critical-result-escalation | ENGINE + ADAPTER (shared Novu) + BUILD | 3rd confirmed Novu reuse; threshold rules and escalation state machine are platform-owned patient-safety logic | — |
| 62 | 2026-07-16 | Result Verification and Reporting | result-amendment-workflow | REFERENCE (FHIR DiagnosticReport) + ENGINE + ADAPTER (shared OPA) + BUILD | 6th confirmed OPA reuse; versioned-amendment workflow is Core Domain, no product exists outside a whole LIMS | — |
| 63 | 2026-07-16 | Quality Management | capa-management | BUILD | No credible open-source CAPA product survives verification; a named candidate (QDMS) was found to be a name collision with an unrelated financial-data project | — |
| 64 | 2026-07-16 | Quality Management | complaint-management | BUILD | Same evidence base as capa-management; generic helpdesk tools are a category mismatch | — |
| 65 | 2026-07-16 | Quality Management | nonconformance-tracking | BUILD | Same evidence base; integrates directly with Module 14's execution Aggregates | — |
| 66 | 2026-07-16 | Quality Management | accreditation-tracking | BUILD | Eramba (Module 3) considered and rejected as a category mismatch (infosec GRC, not lab accreditation) | — |
| 67 | 2026-07-16 | Asset and Maintenance | asset-registry | ENGINE + ADAPTER: Atlas CMMS | 1st genuine whole-system Engine adoption outside the Core Domain cluster — not Core-Domain-adjacent, so no ADR-0011 conflict; openMAINT credible fallback | — |
| 68 | 2026-07-16 | Asset and Maintenance | preventive-maintenance-scheduling | ENGINE + ADAPTER (shared Atlas CMMS) | Native PM module | — |
| 69 | 2026-07-16 | Asset and Maintenance | calibration-management | ENGINE + ADAPTER (shared Atlas CMMS) | Native PM-task-type; explicitly not a duplicate of Module 14's analyzer-tied calibration-tracking | — |
| 70 | 2026-07-16 | Asset and Maintenance | spare-parts-tracking | ENGINE + ADAPTER (shared Atlas CMMS), TENTATIVE | Native Parts module; flagged as a potential Detected Duplicate against Module 18 (Inventory), pending reconciliation | — |
| 71 | 2026-07-16 | Inventory | stock-management | ENGINE + ADAPTER: OpenBoxes (EPL-1.0) | Healthcare-purpose-built (Partners In Health), cleanest license in program; **supersedes row 70** — resolves Module 17's spare-parts-tracking duplicate | Supersedes row 70 |
| 72 | 2026-07-16 | Inventory | warehouse-management | ENGINE + ADAPTER (shared OpenBoxes) | Native Facility/Location hierarchy | — |
| 73 | 2026-07-16 | Inventory | expiry-batch-tracking | ENGINE + ADAPTER (shared OpenBoxes) | FEFO/lot/expiry was the primary decision driver for OpenBoxes | — |
| 74 | 2026-07-16 | Inventory | barcode-scanning | LIBRARY (shared ZXing) + ENGINE + ADAPTER (shared OpenBoxes) + BUILD | Composes 2 already-decided capabilities, no new search needed | — |
| 75 | 2026-07-16 | Inventory | cold-chain-tracking | ENGINE + ADAPTER (shared OpenBoxes) + BUILD (sensor telemetry) | No credible open-source cold-chain IoT platform survived verification (only personal/student projects found); correctly rejected, not force-fit | — |
| 76 | 2026-07-16 | Procurement | purchase-requisition-order | ENGINE + ADAPTER: ERPNext (GPL-3.0) | Purpose-built requisition→RFQ→PO→approval chain; OpenProcurement rejected as government-tender-scale mismatch | — |
| 77 | 2026-07-16 | Procurement | supplier-rfq | ENGINE + ADAPTER (shared ERPNext) | Native RFQ-to-Supplier-Portal flow | — |
| 78 | 2026-07-16 | Procurement | receiving-goods | ENGINE + ADAPTER (composed: ERPNext + OpenBoxes) | ERPNext handles PO/receipt matching, OpenBoxes handles the actual stock increase — a proactively-designed avoidance of a 3rd Detected Duplicate | — |
| 79 | 2026-07-16 | Supplier Management | supplier-registry-evaluation | ENGINE + ADAPTER (shared ERPNext) | Native Supplier Scorecard, confirmed via search; gates Module 19's RFQ/PO eligibility directly | — |
| 80 | 2026-07-16 | Supplier Management | contract-management | ENGINE + ADAPTER (shared ERPNext) | Native Contract doctype; alerting routed through Novu (Module 5) rather than ERPNext's own email alerts | — |
