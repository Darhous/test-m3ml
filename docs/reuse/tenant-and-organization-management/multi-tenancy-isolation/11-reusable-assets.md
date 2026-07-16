# Reusable Assets — Multi-Tenancy Isolation

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| Data Model | `tenant_id` column + RLS policy pattern | PostgreSQL / 2026 industry-consensus SaaS architecture guides | Directly reusable schema convention for every tenant-scoped Aggregate across all 28 Bounded Contexts. |
| Workflow | Session-variable propagation from auth token to RLS context | Composed from Module 1 (Keycloak) + this Feature's research | Closes the loop between authentication and data-level enforcement — a concrete, reusable integration recipe. |
