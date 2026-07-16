# Feature: Organization / Branch Hierarchy

**Module:** Tenant and Organization Management (Platform Kernel).
Modeling and managing the Organization → Branch structure within a
tenant (a lab chain's multiple physical locations, a hospital's
departments — per Wave 3's "Branch Management" capability). Directly
reuses Module 1's `user-group-management` Feature's Keycloak nested-
Group decision (already selected there) — no new research needed for the
identity-side hierarchy; this Feature's own scope is the **business data**
side (Branch address, operating hours, licensing info — not identity).
