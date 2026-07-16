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
| Audit and Compliance | immutable-audit-trail | ENGINE + ADAPTER | immudb | High — cryptographic tamper-evidence vs. Risk #25 | Decided |
| Audit and Compliance | consent-management | REFERENCE (FHIR) + BUILD (enforcement via OPA) | N/A — no engine exists for this exact scope | Medium | Decided |
| Audit and Compliance | policy-engine | ENGINE + ADAPTER (shared) | OPA (shared with Identity and Access) | Medium — avoids a 2nd policy engine | Decided |
| Audit and Compliance | compliance-tracking | ENGINE + ADAPTER (low confidence) | Eramba Community (tentative) | Low-Medium — flagged for reconsideration | Decided (tentative) |
| Audit and Compliance | document-control | CONSOLIDATED — see Document Management | Deferred | TBD | Deferred to Module 8 |
| Device Integration Gateway | hl7-integration-engine | ENGINE + ADAPTER (caveated) | Mirth 4.5.2 (frozen OSS) or Apache Camel fallback | Medium-High, offset by frozen-security risk | Decided (tentative) |
| Device Integration Gateway | astm-integration | ENGINE + ADAPTER (shared) + BUILD (parsing) | Same as hl7-integration-engine | Medium | Decided |
| Device Integration Gateway | device-protocol-adapters | BUILD (per-vendor, on shared engine) | N/A | Low per-adapter | Decided |
| Device Integration Gateway | message-broker-queueing | ENGINE + ADAPTER | RabbitMQ | High — resolves 2 prior Modules' deferred durability requirement | Decided |
| Notification Service | multi-channel-notification-engine | ENGINE + ADAPTER (license pending) | Novu | High — avoids N vendor SDK integrations | Decided (license TBC) |
| Notification Service | templating | ENGINE + ADAPTER (shared) | Novu | Medium | Decided |
| Notification Service | delivery-tracking | ENGINE + ADAPTER (shared) | Novu | Medium | Decided |
| Notification Service | whatsapp-integration | ENGINE + ADAPTER (shared) + SDK (BSP, vendor TBD) | Novu + BSP | Medium | Decided |
| AI Operations Gateway | llm-gateway-orchestration | ENGINE + ADAPTER | Portkey | High | Decided |
| AI Operations Gateway | prompt-audit-logging | ENGINE + ADAPTER (composed) | Portkey + immudb | Medium | Decided |
| AI Operations Gateway | ai-use-case-governance | ENGINE + ADAPTER (composed) | Portkey + OPA | High — clinical-safety-adjacent | Decided |
| AI Operations Gateway | semantic-search | REFERENCE/LIBRARY | pgvector | High — avoids a dedicated vector DB service | Decided |
| Analytics | bi-dashboards | ENGINE + ADAPTER | Apache Superset | High — decisive White-Label fit | Decided |
| Analytics | embedded-analytics | ENGINE + ADAPTER (shared) | Apache Superset | High | Decided |
| Analytics | reporting-engine | ENGINE + ADAPTER (composed) | Superset + Novu | Medium | Decided |
| Analytics | forecasting-engine | LIBRARY | Prophet | Low-Medium (speculative capability) | Decided |
| Document Management | document-storage-versioning | ENGINE + ADAPTER | Alfresco Community (license TBC) | High | Decided |
| Document Management | document-control-workflow | ENGINE + ADAPTER (shared) | Alfresco Community | High — resolves Module 3's deferred duplicate | Decided |
| Document Management | e-signature | ENGINE + ADAPTER | Documenso (license TBC) | Medium-High | Decided |
| Audit and Compliance | document-control | *(superseded — see Document Management `document-control-workflow`)* | Alfresco Community | — | Resolved |
