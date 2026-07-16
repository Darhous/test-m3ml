# Integration Options — BI Dashboards

Superset deployed as a Shared Technical Service (Wave 10) reading from
the platform's PostgreSQL (read-replica recommended at SAD time), scoped
per-tenant via Superset's own RLS features aligned to Module 2's
`tenant_id` convention. Embedded into tenant Portals via Superset's
embedding SDK for the White-Label requirement.
