# Build vs. Buy — Semantic Search

| Dimension (Weight) | pgvector | Qdrant | Weaviate | Build |
|---|---|---|---|---|
| Architecture (15%) | 5 — reuses existing DB | 4 | 4 | 1 |
| Security (15%) | 5 — inherits Postgres | 4 | 4 | 1 |
| License (10%) | 5 | 5 | 5 | 5 |
| Community (10%) | 5 | 4 | 4 | N/A |
| Healthcare Suitability (10%) | 4 — tenant isolation for free | 3 | 3 | Unknown |
| Vendor Independence (5%) | 5 | 4 | 3 | 5 |

**Weighted (approx):** pgvector **4.7**, Qdrant **4.0**, Weaviate **3.8**,
Build **~1.5**. **Conclusion: pgvector** — the clearest "reuse what you
already have" case in the entire program, per Constitution Section 55's
evidence-based extraction/addition triggers (no measured need for a
dedicated vector database yet).
