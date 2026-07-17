# Master Cross-Feature Dependency Map

Detects repositories that solve **multiple** Features at once, so research
is never duplicated. When a candidate reappears in a later Feature's
research, this file is checked first and the entry is cross-referenced,
not re-derived. Example (from the program's own instructions): Keycloak
solves Authentication, Authorization, SSO, MFA, Session Management, and
Audit-adjacent identity events — one adoption decision, five Feature
entries pointing back to it.

| Repository | Features It Solves | Modules | Single Adoption Point (which Feature owns the decision) |
|---|---|---|---|
| Keycloak | authentication, sso-oidc-oauth, multi-factor-auth, session-management, user-group-management, authorization-rbac-abac (coarse RBAC layer), audit-hooks-integration (adapter target) | Identity and Access | `authentication` (`identity-and-access/authentication/10-final-decision.md`) — all other Features cross-reference this decision rather than re-deriving it |
| Open Policy Agent | authorization-rbac-abac (fine-grained ABAC layer) | Identity and Access | `authorization-rbac-abac` |
| PostgreSQL RLS | multi-tenancy-isolation | Tenant and Organization Management | `multi-tenancy-isolation` |
| Unleash | feature-flags, tenant-configuration (simple values) | Tenant and Organization Management | `feature-flags` |
| Open Policy Agent | authorization-rbac-abac (Identity and Access), policy-engine (Audit and Compliance) | Identity and Access, Audit and Compliance | `authorization-rbac-abac` (Module 1) — 2nd Module now reuses this engine, no re-decision |
| immudb | immutable-audit-trail | Audit and Compliance | `immutable-audit-trail` |
| Alfresco Community | document-storage-versioning, document-control-workflow (resolves Module 3's deferred `document-control`) | Document Management | `document-storage-versioning` |
| immudb | immutable-audit-trail (Audit and Compliance), chain-of-custody (Specimen Operations) | Audit and Compliance, Specimen Operations | `immutable-audit-trail` (Module 3) — 2nd Module now reuses this integrity store |
| HL7 FHIR resource patterns (Patient/Practitioner/ServiceRequest-Task/Encounter/Specimen) | patient-registry-mpi, practitioner-registry-credentialing, referral-management, encounter-tracking, order-entry-cpoe, order-status-tracking, specimen-accessioning, worklist-management | Patient Management, Practitioner and Clinic Management, Scheduling and Encounters, Diagnostic Ordering, Specimen Operations, Laboratory Execution | `patient-registry-mpi` (Module 9) — establishes the Core-Domain-preserving REFERENCE+BUILD pattern reused across 6 subsequent Modules |
| Mirth Connect / Apache Camel | hl7-integration-engine, astm-integration (Device Integration Gateway), analyzer-middleware-integration (Laboratory Execution) | Device Integration Gateway, Laboratory Execution | `hl7-integration-engine` (Module 4) — 2nd Module now reuses this engine for analyzer-specific traffic |
| Open Policy Agent | authorization-rbac-abac (Identity and Access), policy-engine, consent-management enforcement (Audit and Compliance), ai-use-case-governance (AI Operations Gateway), result-review-verification-workflow, result-amendment-workflow (Result Verification and Reporting) | Identity and Access, Audit and Compliance, AI Operations Gateway, Result Verification and Reporting | `authorization-rbac-abac` (Module 1) — 6th confirmed reuse, the strongest Cross-Feature Dependency case in the program |
| Novu | multi-channel-notification-engine, templating, delivery-tracking, whatsapp-integration (Notification Service), reminders-integration (Scheduling and Encounters), critical-result-escalation (Result Verification and Reporting) | Notification Service, Scheduling and Encounters, Result Verification and Reporting | `multi-channel-notification-engine` (Module 5) — 3rd Module now reuses this engine |
| Atlas CMMS | asset-registry, preventive-maintenance-scheduling, calibration-management | Asset and Maintenance | `asset-registry` (Module 17) — 3 Features (spare-parts-tracking superseded, see OpenBoxes row below) |
| OpenBoxes | stock-management, warehouse-management, expiry-batch-tracking, barcode-scanning (shared), cold-chain-tracking, spare-parts-tracking (supersedes Atlas CMMS's tentative Parts module) | Inventory, Asset and Maintenance | `stock-management` (Module 18) — single Adoption Point for all platform stock/consumable tracking |
| ZXing | barcode-labeling (Specimen Operations), barcode-scanning (Inventory) | Specimen Operations, Inventory | `barcode-labeling` (Module 13) — 2nd Module now reuses this library |
| ERPNext | purchase-requisition-order, supplier-rfq, receiving-goods (composed with OpenBoxes) (Procurement), supplier-registry-evaluation, contract-management (Supplier Management), invoicing-engine, pricing-price-lists, collections-dunning (Billing) | Procurement, Supplier Management, Billing | `purchase-requisition-order` (Module 19) — now spans 3 Modules, the broadest single-Engine footprint in the program after Keycloak |
| OpenBoxes | stock-management, warehouse-management, expiry-batch-tracking, barcode-scanning, cold-chain-tracking (Inventory), spare-parts-tracking (Asset and Maintenance), receiving-goods stock-increase step (Procurement) | Inventory, Asset and Maintenance, Procurement | `stock-management` (Module 18) — 3rd Module now reuses this Engine |

## Detected Duplicate Features (Consolidation Opportunities)

| Feature A | Feature B | Finding | Status / Resolution |
|---|---|---|---|
| Audit and Compliance `document-control` | Document Management `document-control-workflow` | Same underlying capability (versioned, approval-gated document lifecycle), described from two angles (Governance/SOP vs. general-purpose) | **Resolved at Module 8** — Alfresco Community Edition (Activiti workflow engine) selected once, serving both Feature framings. See `document-management/document-control-workflow/10-final-decision.md`. |
| Asset and Maintenance `spare-parts-tracking` (Atlas CMMS Parts module) | Inventory `stock-management` (OpenBoxes) | Both may need to own maintenance/general stock levels — potential overlap | **Resolved at Module 18** — OpenBoxes is the platform's single stock-management Adoption Point; Atlas CMMS integrates with it via API for parts consumption rather than maintaining a parallel ledger. See `inventory/stock-management/09-integration-options.md`. |
| Procurement `receiving-goods` (ERPNext's native stock module) | Inventory `stock-management` (OpenBoxes) | ERPNext ships its own stock module, which could compete with OpenBoxes as system-of-record | **Avoided proactively at Module 19** — ERPNext handles only PO/receipt matching; the stock-increase call goes to OpenBoxes, never touching ERPNext's own stock module. See `procurement/receiving-goods/09-integration-options.md`. |
| Billing `pricing-price-lists` (ERPNext Pricing Rules) | Diagnostic Ordering `order-catalog-pricing` (Module 12, platform-owned BUILD) | Both touch "pricing" — could be mistaken for the same concern | **Avoided proactively at Module 21** — Module 12 owns the catalog list price (Core-Domain-adjacent BUILD); ERPNext Pricing Rules apply commercial discounts on top, a distinct layer, not a duplicate. See `billing/pricing-price-lists/09-integration-options.md`. |
