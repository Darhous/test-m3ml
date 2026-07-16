# License Review — Multi-Tenancy Isolation

| Candidate | License | Compatibility |
|---|---|---|
| PostgreSQL RLS | PostgreSQL License (permissive, similar to MIT/BSD) — part of PostgreSQL core itself | **Clear** |
| Citus | AGPL 3.0 (community edition, `citusdata/citus`) | **Conditional** — same network-use consideration already surfaced for Zitadel in Module 1; would need re-evaluation if/when sharding is actually justified, not relevant at current evidenced scale |

No license blocker for the recommended default (native Postgres RLS
requires no separate license at all, since it ships with PostgreSQL
itself, which the platform has not yet formally selected but which is
the overwhelmingly likely candidate given the rest of this research's
Postgres-centric findings — noted as an observation, not a Technology
Selection, which remains out of this program's scope).
