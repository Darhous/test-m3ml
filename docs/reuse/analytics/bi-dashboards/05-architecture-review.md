# Architecture Review — BI Dashboards

Superset connects to the platform's own PostgreSQL (read replicas
recommended at SAD time to avoid OLAP-query contention with OLTP
traffic) via standard SQL — no separate data-pipeline product required
at this platform's evidenced scale. Row-level security integration
(Superset supports RLS-aware dashboards) composes with Module 2's
tenant-isolation pattern for safe multi-tenant BI.
