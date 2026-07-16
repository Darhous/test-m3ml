# Security Review — Multi-Tenancy Isolation

PostgreSQL RLS is a mature, long-standing core database feature (not a
bolt-on extension), inheriting PostgreSQL's own extensive security
track record and disclosure process (PostgreSQL Security Team, CVE-
tracked). No RLS-specific CVE pattern surfaced in this search round.
Known real-world failure mode (industry-documented, not specific to any
one vendor): RLS policies silently not applying to a database superuser
or a connection that fails to set the tenant-context session variable —
this is a **configuration-correctness risk**, not a product
vulnerability, and must be covered by the platform's own Multi-Tenant
Isolation Testing (Constitution Section 36, already Required) rather than
assumed safe by default.
