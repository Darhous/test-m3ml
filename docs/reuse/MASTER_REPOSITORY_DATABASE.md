# Master Repository Database

Every distinct repository/project identified anywhere in this program,
deduplicated (a repository solving multiple Features is listed once here
and cross-referenced from each Feature it touches — see "Features Solved"
column). Populated incrementally as each Module completes; see
`MASTER_FEATURE_CATALOG.md` for what remains outstanding.

| Repository | Org/Vendor | License | Latest Activity | Features Solved (this program) | Modules Touched |
|---|---|---|---|---|---|
| Keycloak (`keycloak/keycloak`) | Red Hat/IBM, CNCF Incubating | Apache-2.0 | Active — 26.5.7, April 2026 | authentication, sso-oidc-oauth, multi-factor-auth, session-management, user-group-management, audit-hooks-integration (adapter target), authorization-rbac-abac (coarse RBAC layer) | Identity and Access |
| Open Policy Agent (`open-policy-agent/opa`) | CNCF Graduated | Apache-2.0 | Active | authorization-rbac-abac (fine-grained ABAC layer) | Identity and Access |
| Zitadel (`zitadel/zitadel`) | ZITADEL GmbH | AGPL-3.0 (core, since 2025) | Active | Evaluated, not selected — `authentication`/`sso-oidc-oauth` alternative | Identity and Access |
| Authentik (`goauthentik/authentik`) | Authentik Security | MIT (core) + Enterprise commercial tier | Active | Evaluated, not selected — `authentication`/`sso-oidc-oauth` alternative | Identity and Access |
| Ory Kratos + Hydra (`ory/kratos`, `ory/hydra`) | Ory Corp | Apache-2.0 | Active — Hydra OIDF-certified | Evaluated, not selected — `authentication`/`sso-oidc-oauth` alternative | Identity and Access |
| Casbin (`casbin/casbin`) | Community | Apache-2.0 | Active | Evaluated, not selected (close second) — `authorization-rbac-abac` alternative | Identity and Access |
