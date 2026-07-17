# Master Reuse Matrix

Every reusable asset identified across all Features — not just the
adopted candidate, but any Data Model, Workflow, UI Pattern, or API
Design worth reusing even when the Feature's overall decision is BUILD.
Detail lives in each Feature's `11-reusable-assets.md`.

| Module | Feature | Asset Type (Data Model / Workflow / UI Pattern / API Design) | Source | Reuse Note |
|---|---|---|---|---|
| Identity and Access | authentication | Data Model | Keycloak Realm/Organization/User/Group/Role schema | Informs the platform's own Identity Aggregate design |
| Identity and Access | authentication | Workflow | OIDC Authorization Code + PKCE login flow | Canonical login sequence, no need to design from scratch |
| Identity and Access | authentication | API Design | OIDC Discovery Document / standard OAuth2/OIDC endpoints | Reference shape for the platform's own Identity contract |
| Identity and Access | authentication | UI Pattern | Keycloak themeable login/MFA/recovery screens | Reskinnable for White-Label, full custom theming needs SAD evaluation |
| Identity and Access | sso-oidc-oauth | Workflow | Identity Brokering claim-mapping | Onboarding a customer's existing corporate IdP |
| Identity and Access | sso-oidc-oauth | API Design | OAuth2 Client-Credentials grant | Partner/API client machine-to-machine auth |
| Identity and Access | user-group-management | Data Model | Nested Group hierarchy with inherited roles | Direct structural match for Organization → Branch → Staff |
| Identity and Access | authorization-rbac-abac | Data Model | Rego input-document schema pattern | Structures the 8-dimension Policy Model's input document |
| Identity and Access | authorization-rbac-abac | Workflow | Policy-decision-with-trace evaluation | Reusable audit-trace shape for every Sensitive-Operation decision |
| Tenant and Organization Management | multi-tenancy-isolation | Data Model | `tenant_id` + RLS policy pattern | Reusable schema convention across all 28 Bounded Contexts |
| Tenant and Organization Management | feature-flags | API Design | OpenFeature evaluation API | Vendor-neutral internal flag-evaluation contract |
| Tenant and Organization Management | feature-flags | Workflow | 4-eyes change-approval flow | Template for candidate "Elevated Audit" governance tier |
| Tenant and Organization Management | tenant-provisioning | Workflow | Saga with compensation | Reusable pattern for other multi-step cross-Module workflows |
| Audit and Compliance | immutable-audit-trail | Data Model | immudb cryptographically-linked record structure | Informs the platform's own Audit Event schema |
| Audit and Compliance | consent-management | Data Model | FHIR `Consent` resource shape | Directly reusable as the Consent Aggregate structure |
| Patient Management | patient-registry-mpi | Data Model | FHIR `Patient` resource | Reused as a Reference pattern across 6 subsequent Modules (9-14) |
| Diagnostic Ordering | order-entry-cpoe | Workflow | FHIR ServiceRequest/Task order-orchestration pattern | Cross-validated by 2 independent production systems (OpenELIS Global, Bahmni) |
| Laboratory Execution | quality-control-tracking | Workflow | Westgard rules statistical QC methodology | Public, non-proprietary, industry-standard — not tied to any product |
| Result Verification and Reporting | result-review-verification-workflow | Workflow | Policy-decision-with-trace evaluation (reused from Identity and Access) | Same audit-trace shape applied to the 8-dimension Result Verification Policy Model |
| Payroll | payroll-approval-dual-control | Workflow | 4-eyes change-approval flow (reused from Tenant and Organization Management) | Same dual-control pattern applied to payroll disbursement |

**Scope note (final):** Row-by-row cataloguing at Modules 1-3's density
was not sustained across all 28 Modules per the pacing instruction — the
5 rows above are the most consequential cross-Module reuse patterns
found in the remaining 25 Modules, not an exhaustive re-listing. Every
Feature's complete reusable-asset finding (including ones not
highlighted here) lives in that Feature's own `11-reusable-assets.md` —
the authoritative per-Feature record.
