# Risk Analysis — BI Dashboards

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| OLAP dashboard queries contend with OLTP production traffic on the same PostgreSQL instance | Medium | Medium | Read-replica architecture, an SAD-level decision flagged here |
| Misconfigured Superset RLS leaks cross-tenant analytics data | Low-Medium | High (Risk #17-class) | Superset RLS rules must be generated/verified against the platform's own tenant model, not manually maintained in parallel |
