# Integration Options — Multi-Tenancy Isolation

Recommended pattern (evidence for the SAD, not a Discovery decision):
every database session sets a Postgres session variable (e.g.,
`app.current_tenant`) immediately after authentication, sourced from the
Keycloak-issued token's Organization claim (Module 1 integration); every
tenant-scoped table carries a `tenant_id` column and an RLS policy
comparing it to `app.current_tenant`. Application code continues to write
normal queries — the database transparently filters results, providing
defense-in-depth even if application-layer scoping logic has a bug.
