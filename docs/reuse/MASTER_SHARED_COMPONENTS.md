# Master Shared Components Register

Components that, once adopted for one Feature, should be reused as
shared infrastructure across multiple Modules rather than adopted
independently per Module (e.g., a single Keycloak realm-per-tenant setup
serving every Business Module's authentication need, not one per Module).

| Shared Component | Candidate | Serves (Modules/Features) | Why Shared, Not Per-Module |
|---|---|---|---|
