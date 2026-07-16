# Final Decision — Multi-Tenancy Isolation

## Decision: **REFERENCE**

Reuse the industry-consensus architecture pattern (shared schema +
`tenant_id` + PostgreSQL Row-Level Security) as the evidence-based
Reference design for the Shared tier of ADR 0005's already-Accepted
Hybrid model. This is offered as research evidence toward resolving
`open-questions.md` #15 — **this program does not itself resolve #15**;
that remains the user's/Architecture Review Board's decision at SAD time,
per this program's own scope boundary (Build-vs-Buy/Reuse research, not
architectural decision-making).

## Why Not Schema-Per-Tenant

Higher operational cost (N-times migrations) with no measured need
(Constitution Section 55) for its stronger isolation at this platform's
current evidenced scale — the Dedicated tier already exists in ADR 0005
for tenants that genuinely need stronger-than-RLS isolation.

## Why Not a Third-Party Library/Product

None credible was found — the effective mechanism (RLS) is a database-
native capability, not third-party software. This is itself a finding:
not every Feature in this program resolves to "adopt Product X."
