# Master Build-vs-Buy Matrix

The single final decision for every Feature — exactly one of **BUILD /
CONTROLLED FORK / ENGINE + ADAPTER / SDK / LIBRARY / REFERENCE / REJECT**
per the program's Final Decision categories. Full reasoning lives in each
Feature's own `10-final-decision.md`; this is the roll-up index.

| Module | Feature | Decision | Primary Candidate (if not BUILD) | Estimated Effort Saved | Status |
|---|---|---|---|---|---|
| Identity and Access | authentication | ENGINE + ADAPTER | Keycloak | Not numerically estimated (No-Guessing Rule) — qualitatively High, universal-dependency Feature | Decided |
| Identity and Access | sso-oidc-oauth | ENGINE + ADAPTER | Keycloak (same Engine) | High | Decided |
| Identity and Access | multi-factor-auth | ENGINE + ADAPTER | Keycloak (same Engine) | Medium-High | Decided |
| Identity and Access | session-management | ENGINE + ADAPTER | Keycloak (same Engine) | Medium-High | Decided |
| Identity and Access | user-group-management | ENGINE + ADAPTER | Keycloak (same Engine) | Medium | Decided |
| Identity and Access | authorization-rbac-abac | ENGINE + ADAPTER (dual: Keycloak RBAC + OPA ABAC) | OPA (new engine) + Keycloak (existing) | High — clinical-safety-adjacent, Wave 6 Policy Model | Decided |
| Identity and Access | audit-hooks-integration | LIBRARY (thin adapter over Keycloak SPI) | N/A — platform-owned glue | Low (small, but avoids reinventing event delivery) | Decided |
| Tenant and Organization Management | tenant-provisioning | BUILD (orchestration; calls existing Engines) | N/A | Low (small, but avoids ad-hoc per-Module provisioning code) | Decided |
| Tenant and Organization Management | organization-branch-hierarchy | BUILD | N/A | Low | Decided |
| Tenant and Organization Management | multi-tenancy-isolation | REFERENCE (PostgreSQL RLS pattern) | PostgreSQL (built-in) | High — avoids building custom row-filtering logic; evidence for `open-questions.md` #15 | Decided |
| Tenant and Organization Management | feature-flags | ENGINE + ADAPTER | Unleash (via OpenFeature) | Medium-High | Decided |
| Tenant and Organization Management | tenant-configuration | ENGINE + ADAPTER (shared) + BUILD (complex config) | Unleash (shared with feature-flags) | Medium | Decided |
