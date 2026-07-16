Inherits `../bi-dashboards/06-security-review.md`. Scheduled-report
recipients must be validated against the requesting user's own RLS
scope, not an admin-configurable arbitrary email list, to avoid a
cross-tenant data-leak vector.
