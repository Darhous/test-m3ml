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
| 8 | 2026-07-16 | Tenant and Organization Management | tenant-provisioning | BUILD: orchestration Saga over Keycloak + PostgreSQL | Platform-specific workflow, no product fits | — |
| 9 | 2026-07-16 | Tenant and Organization Management | organization-branch-hierarchy | BUILD: platform-owned business-data schema | Core domain modeling, not infrastructure | — |
| 10 | 2026-07-16 | Tenant and Organization Management | multi-tenancy-isolation | REFERENCE: PostgreSQL Row-Level Security pattern | Industry-consensus default; database-native, no product to adopt; evidence for `open-questions.md` #15, not a resolution | — |
| 11 | 2026-07-16 | Tenant and Organization Management | feature-flags | ENGINE + ADAPTER: Unleash via OpenFeature | Governance/audit features fit Sensitive-Operation-adjacent gating; regulated-sector adoption evidence | — |
| 12 | 2026-07-16 | Tenant and Organization Management | tenant-configuration | ENGINE + ADAPTER (shared Unleash) + BUILD (complex config) | Avoids a second flag/config engine (Flagsmith rejected for this reason specifically) | — |
| 13 | 2026-07-16 | Audit and Compliance | immutable-audit-trail | ENGINE + ADAPTER: immudb | Cryptographic tamper-evidence, holds even against a malicious DBA; explicit 2026 healthcare framing | — |
| 14 | 2026-07-16 | Audit and Compliance | consent-management | REFERENCE (FHIR Consent) + BUILD (enforcement via OPA) | No dedicated clinical-consent engine exists; Klaro-class tools are website/cookie consent, a real category mismatch, not force-fit | — |
| 15 | 2026-07-16 | Audit and Compliance | policy-engine | ENGINE + ADAPTER (shared OPA) | Same engine as Identity and Access `authorization-rbac-abac`, 2nd consuming Module | — |
| 16 | 2026-07-16 | Audit and Compliance | compliance-tracking | ENGINE + ADAPTER: Eramba Community (tentative, low confidence) | Weakest-evidence decision in the program so far; explicitly flagged for SAD-level reconsideration | — |
| 17 | 2026-07-16 | Audit and Compliance | document-control | CONSOLIDATED — deferred to Document Management | Detected duplicate of Document Management's `document-control-workflow`; avoids duplicate research | — |
| 18 | 2026-07-16 | Device Integration Gateway | hl7-integration-engine | ENGINE + ADAPTER (tentative): Mirth 4.5.2, Camel fallback | Best healthcare-purpose fit, but frozen since NextGen's March 2025 licensing change — explicitly flagged | — |
| 19 | 2026-07-16 | Device Integration Gateway | astm-integration | ENGINE + ADAPTER (shared) + BUILD | Follows hl7-integration-engine; weak native ASTM tooling on both candidates | — |
| 20 | 2026-07-16 | Device Integration Gateway | device-protocol-adapters | BUILD | No product exists per-vendor by definition | — |
| 21 | 2026-07-16 | Device Integration Gateway | message-broker-queueing | ENGINE + ADAPTER: RabbitMQ | Durable, moderate-scale fit; resolves 2 prior Modules' deferred delivery-guarantee questions | — |
| 22 | 2026-07-16 | Notification Service | multi-channel-notification-engine | ENGINE + ADAPTER: Novu (license TBC) | Only credible self-hostable OSS multi-channel engine found; Courier/Knock/SuprSend are SaaS-first | — |
| 23 | 2026-07-16 | Notification Service | templating | ENGINE + ADAPTER (shared Novu) | Built-in per-channel template editor | — |
| 24 | 2026-07-16 | Notification Service | delivery-tracking | ENGINE + ADAPTER (shared Novu) | Built-in delivery-status tracking | — |
| 25 | 2026-07-16 | Notification Service | whatsapp-integration | ENGINE + ADAPTER (shared Novu) + SDK (BSP, vendor TBD) | Native WhatsApp provider; BSP is a commercial decision, not software Build-vs-Buy | — |
