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
| Tenant and Organization Management | feature-flags, tenant-configuration | Unleash (via OpenFeature) | Custom-built flag/config service, custom rollout-approval workflow | Platform code calls the OpenFeature SDK, not Unleash's proprietary SDK |
| Audit and Compliance | immutable-audit-trail | immudb | A custom cryptographic append-only log implementation | Audit and Compliance Module's own write path only |
| Audit and Compliance | policy-engine | Open Policy Agent (reused) | A second, separate policy engine | Same OPA instance as Identity and Access, separately namespaced bundles |
| Audit and Compliance | compliance-tracking (tentative) | Eramba Community | A custom internal GRC tool | Standalone internal tool, no runtime Module dependency |
| Device Integration Gateway | hl7-integration-engine, astm-integration | Mirth Connect 4.5.2 (frozen, tentative) or Apache Camel | A full custom HL7/ASTM parsing and channel-routing engine | Independent Component (ADR 0006); frozen-OSS risk explicitly flagged |
| Device Integration Gateway | message-broker-queueing | RabbitMQ | A custom durable-queue implementation | Platform-wide Shared Technical Service, not per-Module |
| Notification Service | multi-channel-notification-engine, templating, delivery-tracking, whatsapp-integration | Novu | N separate vendor SDK integrations (Email/SMS/Push/WhatsApp) built and maintained individually | Independent Component (Constitution Section 11); license `Requires Legal Verification` |
