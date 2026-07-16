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
| HL7 FHIR resource patterns (Patient/Practitioner/ServiceRequest-Task/Encounter/Specimen) | patient-registry-mpi, practitioner-registry-credentialing, referral-management, encounter-tracking, order-entry-cpoe, order-status-tracking, specimen-accessioning | Patient Management, Practitioner and Clinic Management, Scheduling and Encounters, Diagnostic Ordering, Specimen Operations | `patient-registry-mpi` (Module 9) — establishes the Core-Domain-preserving REFERENCE+BUILD pattern reused across 5 subsequent Modules |

## Detected Duplicate Features (Consolidation Opportunities)

| Feature A | Feature B | Finding | Resolution |
|---|---|---|---|
| Audit and Compliance `document-control` | Document Management `document-control-workflow` | Same underlying capability (versioned, approval-gated document lifecycle), described from two angles (Governance/SOP vs. general-purpose) | **Resolved at Module 8** — Alfresco Community Edition (Activiti workflow engine) selected once, serving both Feature framings. See `document-management/document-control-workflow/10-final-decision.md`. |
