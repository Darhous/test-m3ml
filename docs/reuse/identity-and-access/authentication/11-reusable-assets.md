# Reusable Assets — Authentication

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| Data Model | Realm / Organization / User / Group / Role schema | Keycloak | Directly informs the platform's own Identity and Access Aggregate design (Wave 9, Context 27) — the platform should model its own `Tenant`/`User`/`Role` concepts congruently with Keycloak's Organization/User/Role primitives to minimize adapter-layer translation complexity. |
| Workflow | Login → MFA challenge (if enabled) → token issuance → refresh-token rotation | Keycloak (standard OIDC Authorization Code + PKCE flow) | Reuse as the platform's own canonical login sequence diagram basis — no need to design this from scratch. |
| API Design | OIDC Discovery Document (`/.well-known/openid-configuration`), standard OAuth2/OIDC endpoints | OpenID Foundation spec, implemented by Keycloak | The platform's Identity and Access Module's own public contract to other Modules should mirror this shape (well-known discovery, standard claim names) rather than invent a bespoke one — directly serves Constitution Section 12/13 (Event/API naming discipline). |
| UI Pattern | Login/MFA-challenge/account-recovery screens (Keycloak's themeable login flow) | Keycloak | Can be reskinned (Keycloak theming) for White-Label requirements (Wave 1) rather than built from scratch, though full custom-brand-per-tenant theming needs its own SAD-level evaluation (see `12-risk-analysis.md`). |
