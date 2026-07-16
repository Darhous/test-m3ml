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
