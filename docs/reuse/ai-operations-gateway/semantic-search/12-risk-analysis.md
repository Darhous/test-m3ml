# Risk Analysis — Semantic Search

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Vector search volume eventually exceeds pgvector's comfortable range (500K-2M+) | Low (no measured need yet) | Low-Medium | Qdrant migration path already identified; revisit only on real measured trigger |
