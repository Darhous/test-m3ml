# Architecture Review — User and Group Management

Keycloak's Group hierarchy (nested groups with inherited role mappings)
maps naturally onto the platform's Organization/Branch hierarchy (Wave 9,
Tenant and Organization Management Context) — a Group-per-Branch,
nested-under-Group-per-Organization structure is a direct, low-custom-
code mapping, not a forced fit. SCIM support gives a standards-based path
for future HR-driven provisioning (Workforce Management Module) rather
than a bespoke integration.
