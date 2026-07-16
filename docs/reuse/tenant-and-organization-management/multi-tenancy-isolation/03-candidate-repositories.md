# Candidate Repositories — Multi-Tenancy Isolation

**Not a single-repository decision** — this Feature is a database-level
architecture pattern, not a standalone product. No credible "10
candidates" exist because the mechanism (Postgres RLS) is a **built-in
database engine feature**, not separate software to adopt. Per this
program's own instruction ("if only three excellent candidates exist,
report three"), the honest count here is smaller still:

| Candidate | Type | What It Is |
|---|---|---|
| PostgreSQL Row-Level Security (RLS) | Database built-in feature (not a repository) | Native Postgres policy engine, enforces tenant filtering at the query-planner level |
| Citus (`citusdata/citus`) | Postgres extension | Distributed Postgres extension supporting tenant-sharded scaling; relevant only if/when the platform's tenant count and per-tenant data volume justify horizontal sharding — not a Day-1 need per Constitution Section 55's evidence-based extraction triggers |
| Language/ORM-level tenant scoping libraries (e.g., a tenant-scoping middleware for whichever backend framework is eventually chosen) | Library | Application-layer enforcement, a defense-in-depth complement to RLS, not a replacement — the specific library is framework-dependent and cannot be named before the SAD's technology selection (Strict Prohibition of this program: no Technology/Framework Selection) |

## Why This Feature's Decision Type Differs From Every Other Feature So Far

This is the first Feature in the program where the honest answer is
**not** "adopt Product X" but "adopt a database-native *pattern*,
optionally reinforced by a library once the backend framework is chosen."
Reported exactly as found, not forced into a product-shaped answer.
