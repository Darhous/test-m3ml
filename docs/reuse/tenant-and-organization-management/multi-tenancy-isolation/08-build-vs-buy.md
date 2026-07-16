# Build vs. Buy — Multi-Tenancy Isolation

Not a traditional weighted-candidate comparison (only one real database-
native pattern was found fit for purpose at evidenced scale). The
relevant comparison is **pattern vs. pattern**, not product vs. product:

| Pattern | Isolation Strength | Operational Cost | Fit at Current Evidenced Scale |
|---|---|---|---|
| Shared schema + RLS | Strong (engine-enforced) | Low | **Best fit** — no measured need for stronger/costlier isolation yet |
| Schema-per-tenant | Stronger | High (N-times migrations, tooling strain) | Not justified without a measured trigger (Constitution Section 55) |
| Database-per-tenant | Strongest | Highest | Already the Dedicated tier in ADR 0005 — not a shared-tier option at all |

## Conclusion

**REFERENCE** — reuse the industry-consensus RLS pattern and design
principle, not a specific third-party product (there is none to adopt;
RLS ships with PostgreSQL). This is explicitly evidence *for* the future
SAD's resolution of `open-questions.md` #15, not a Discovery-bypassing
decision made by this program.
