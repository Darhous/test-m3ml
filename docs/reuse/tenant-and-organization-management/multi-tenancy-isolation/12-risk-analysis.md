# Risk Analysis — Multi-Tenancy Isolation

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| RLS policy missing on a newly added table (a real, common real-world mistake) | Medium | **Severe** — direct Risk #17 realization | Multi-Tenant Isolation Testing (Constitution Section 36) must run as a mandatory gate before any tenant-scoped module ships, testing for exactly this omission, not just testing the happy path |
| A privileged/superuser database connection bypasses RLS (RLS does not apply to table owners/superusers by default in PostgreSQL) | Low-Medium | Severe if exploited | Application connections must use a non-superuser role with RLS enforced; administrative/migration connections must be tightly controlled and audited separately (Constitution Section 21+23) |
| This Reference pattern is mistaken for a final Decision, silently closing `open-questions.md` #15 without the user's actual sign-off | Medium (a real documentation-discipline risk, not a technical one) | High (governance) | This file and `10-final-decision.md` explicitly state the boundary; the Discovery program's own Open Questions Register is the authoritative place #15 gets marked Answered, not this program |

## Overall Risk Rating

**High** — this Feature underpins Risk Register #17, the single Highest-
severity risk carried through the entire Discovery + Gap Closure program.
The Reference pattern found here is strong evidence, not a resolution.
