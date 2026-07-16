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
