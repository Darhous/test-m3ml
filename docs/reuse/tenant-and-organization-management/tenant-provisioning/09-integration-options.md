# Integration Options — Tenant Provisioning

Orchestrated as a Saga owned by the Tenant and Organization Management
Bounded Context, calling: Keycloak Admin REST API (Organization + initial
admin user creation) → platform tenant-registry table insert (RLS
partition activation) → `TenantProvisioned` Domain Event emitted for
downstream Modules (Notification Service, SaaS Commercial Operations) to
react to.
