# Master Engine Catalog

Candidates classified as a full **Engine** (a substantial runtime system
you deploy and adapt via configuration/plugins, e.g., a full LIS, a full
IAM server, a full workflow engine) — as distinct from a Library or SDK.
Cross-references `10-final-decision.md` entries with an ENGINE + ADAPTER
decision.

| Module | Feature | Engine | What It Replaces | Adapter Boundary |
|---|---|---|---|---|
| Identity and Access | authentication, sso-oidc-oauth, multi-factor-auth, session-management, user-group-management | Keycloak | A full custom-built IAM system (credential storage, OIDC/OAuth2/SAML provider, MFA, session store, admin console) | Anti-Corruption Layer inside the Identity and Access Bounded Context — OIDC/OAuth2 + Admin REST API only |
| Identity and Access | authorization-rbac-abac | Open Policy Agent | A custom rules engine for the 8-dimension Configurable Result Verification Policy Model | Called only by the Result Verification and Reporting Module |
