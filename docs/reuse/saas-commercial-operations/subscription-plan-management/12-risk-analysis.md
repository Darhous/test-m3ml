| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Kill Bill's Java/OSGi-plugin architecture and XML plan catalogs carry a steeper learning curve than newer alternatives | Medium | Low-Medium | Lago logged as a fallback if implementation velocity suffers |
| Running a 2nd financial Engine (Kill Bill) alongside ERPNext (Modules 19-24) for a different billing domain (SaaS subscriptions vs. patient/clinic billing) could confuse scope | Low-Medium | Medium | Explicit SAD-level documentation: ERPNext owns patient/clinic/vendor financial transactions, Kill Bill owns the platform's own SaaS subscription revenue — distinct domains, not a duplicate |
