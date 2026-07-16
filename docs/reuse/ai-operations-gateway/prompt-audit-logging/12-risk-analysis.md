# Risk Analysis — Prompt Audit Logging

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Prompt/response logs containing patient context leak across tenants | Low-Medium | High | RLS tenant isolation applied to AI logs, not exempted as "just logs" |
