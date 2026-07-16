# Global Search Log — Multi-Tenancy Isolation

## Query Run

`multi-tenant SaaS data isolation PostgreSQL row-level security vs
schema-per-tenant open source 2026`

## Landscape Notes (2026 industry consensus, real and dated)

Three real architectural patterns, not three products:
1. **Shared schema + `tenant_id` column + Row-Level Security (RLS).**
   Described in multiple independent 2026 sources as "the best default
   for most new B2B SaaS platforms" — one migration serves every tenant,
   low cost per tenant, simple analytics/admin tooling.
2. **Schema-per-tenant** (one Postgres schema per tenant, same database).
   Stronger isolation, easy per-tenant export, but migrations must run
   once per schema and tooling strain grows with tenant count — 2026
   sources describe it as "rarely worth it at scale compared to shared
   schema with tenant_id."
3. **Database-per-tenant.** Reserved for cases where "enterprise
   contracts, HIPAA, or hard noisy-neighbor limits demand physical
   separation" — i.e., exactly the Dedicated tier ADR 0005 already
   defines, not a shared-tier option.

## Direct Relevance to `open-questions.md` #15

The industry-consensus default (RLS + `tenant_id`) maps directly onto one
of the two candidate categories Discovery Phase 09 already narrowed #15
to (`09-tenancy-analysis.md`: "Tenant-identifier column" vs. "Schema-per-
tenant"). This search independently confirms Phase 09's narrowing was
correct and adds a 2026-current industry-consensus lean toward the
tenant-ID-column option specifically for the Shared tier — offered here
as evidence for the eventual SAD decision, not as this program silently
answering #15 on its own authority.
