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
