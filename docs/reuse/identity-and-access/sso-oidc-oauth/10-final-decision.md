# Final Decision — SSO / OIDC / OAuth

## Decision: **ENGINE + ADAPTER** (Keycloak — same Engine as `authentication`)

Single adoption point: this decision does not introduce a second engine.
Keycloak's Identity Brokering (federation) and native OIDC/OAuth2
Provider capability are used as-is. No alternative scored competitively
once the `authentication` Feature's Engine was already selected — running
a second IAM product solely for federation would violate this program's
own duplicate-elimination objective (`MASTER_DEPENDENCY_MATRIX.md`).
