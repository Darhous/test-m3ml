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
| PostgreSQL (Row-Level Security) | PostgreSQL Global Development Group | PostgreSQL License | Active, mature | multi-tenancy-isolation (Reference pattern) | Tenant and Organization Management |
| Citus (`citusdata/citus`) | Microsoft/Citus Data | AGPL-3.0 (community) | Active | Evaluated, not selected (no measured sharding need) — `multi-tenancy-isolation` alternative | Tenant and Organization Management |
| Unleash (`Unleash/unleash`) | Unleash AS | Apache-2.0 (OSS edition) | Active — weekly releases | feature-flags, tenant-configuration (partial) | Tenant and Organization Management |
| Flagsmith (`Flagsmith/flagsmith`) | Flagsmith | BSD-3-Clause | Active | Evaluated, not selected (avoided as a second flag engine) — `feature-flags`/`tenant-configuration` alternative | Tenant and Organization Management |
| OpenFeature (`open-feature/spec`) | CNCF | Apache-2.0 | Active | Vendor-neutral adapter layer for `feature-flags`/`tenant-configuration` | Tenant and Organization Management |
| immudb (`codenotary/immudb`) | Codenotary | Apache-2.0 | Active — 1.11, May 2026 | immutable-audit-trail | Audit and Compliance |
| Trillian (`google/trillian`) | Google | Apache-2.0 | Active | Evaluated, not selected — `immutable-audit-trail` alternative | Audit and Compliance |
| Open Policy Agent (reused) | CNCF Graduated | Apache-2.0 | Active | policy-engine (2nd consuming Module — see MASTER_DEPENDENCY_MATRIX.md) | Audit and Compliance |
| Eramba (`eramba/community`) | Eramba | GPL-3.0 (unverified this pass) | Active | compliance-tracking (low-confidence, flagged for reconsideration) | Audit and Compliance |
| CISO Assistant (`intuitem/ciso-assistant-community`) | intuitem | AGPL-3.0 | Active | Evaluated, close second — `compliance-tracking` alternative | Audit and Compliance |
| GovReady-Q (`GovReady/govready-q`) | GovReady | GPL-3.0 (unverified this pass) | Active | Evaluated, not selected — `compliance-tracking` alternative | Audit and Compliance |
| Mirth Connect 4.5.2 (last OSS) | NextGen (frozen) | MPL 2.0 | **Frozen since March 2025** (4.6+ commercial-only) | hl7-integration-engine, astm-integration (tentative) | Device Integration Gateway |
| Apache Camel | ASF | Apache-2.0 | Active | Evaluated, credible fallback — `hl7-integration-engine` alternative | Device Integration Gateway |
| RabbitMQ (`rabbitmq/rabbitmq-server`) | Broadcom/VMware | MPL 2.0 | Active, mature | message-broker-queueing | Device Integration Gateway |
| Apache Kafka | ASF | Apache-2.0 | Active | Evaluated, not selected (scale mismatch) — `message-broker-queueing` alternative | Device Integration Gateway |
| NATS + JetStream | CNCF | Apache-2.0 | Active | Evaluated, not selected — `message-broker-queueing` alternative | Device Integration Gateway |
| Novu (`novuhq/novu`) | Novu Inc. | Permissive-leaning (unverified this pass) | Active | multi-channel-notification-engine, templating, delivery-tracking, whatsapp-integration | Notification Service |
| Portkey Gateway (`Portkey-AI/gateway`) | Portkey | Apache-2.0 (since March 2026) | Active | llm-gateway-orchestration, prompt-audit-logging, ai-use-case-governance | AI Operations Gateway |
| LiteLLM (`BerriAI/litellm`) | BerriAI | MIT | Active | Evaluated, close alternative — `llm-gateway-orchestration` | AI Operations Gateway |
| Langfuse (`langfuse/langfuse`) | Langfuse | MIT core | Active | Evaluated, complementary observability layer | AI Operations Gateway |
| pgvector (`pgvector/pgvector`) | PostgreSQL community | PostgreSQL License | Active | semantic-search | AI Operations Gateway |
| Qdrant | Qdrant | Apache-2.0 | Active | Evaluated, identified upgrade path — `semantic-search` | AI Operations Gateway |
| Weaviate | Weaviate | BSD-3-Clause | Active | Evaluated, not selected — `semantic-search` | AI Operations Gateway |
| Apache Superset | ASF | Apache-2.0 | Active | bi-dashboards, embedded-analytics, reporting-engine | Analytics |
| Metabase | Metabase Inc. | AGPL-3.0 (Community) | Active | Evaluated, not selected (paywalled white-label) — `bi-dashboards` | Analytics |
| Lightdash | Lightdash | MIT | Active | Evaluated, not selected — `bi-dashboards` | Analytics |
| Prophet (`facebook/prophet`) | Meta | MIT | Active | forecasting-engine | Analytics |
| Alfresco Community Edition | Alfresco/Hyland | LGPL v3 (unverified this pass) | Active | document-storage-versioning, document-control-workflow (resolves Module 3's `document-control`) | Document Management |
| Nextcloud Hub | Nextcloud GmbH | AGPL-3.0 | Active | Evaluated, not selected — `document-storage-versioning` | Document Management |
| Documenso | Documenso | Unconfirmed this pass | Active | e-signature | Document Management |
| OpenSign | OpenSign Labs | AGPL-3.0 | Active | Evaluated, credible free fallback — `e-signature` | Document Management |
| HL7 FHIR `Patient` resource | HL7 International | HL7 FHIR License | Active | patient-registry-mpi (Reference) | Patient Management |
| OpenCR | Jembi/OpenHIE | Apache-2.0 | Active | Evaluated, identified future upgrade path — `patient-registry-mpi` | Patient Management |
| OpenMRS | OpenMRS community | MPL 2.0 | Active | Evaluated, explicitly not selected (would displace Core Domain) — `patient-registry-mpi` | Patient Management |
| Cal.com | Cal.com Inc. | AGPL-3.0 (core) | Active | appointment-scheduling-engine | Scheduling and Encounters |
| Cal.diy | Community fork | MIT | Active | Evaluated, credible fallback — `appointment-scheduling-engine` | Scheduling and Encounters |
| FullCalendar | FullCalendar | MIT (core) | Active | resource-calendar | Scheduling and Encounters |
