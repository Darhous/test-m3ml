# Global Search Log — Semantic Search

**Query:** `open source vector database pgvector vs Qdrant vs Weaviate
semantic search 2026`

**Finding:** pgvector — a PostgreSQL extension, vectors live in the same
database already selected (Module 2) — "no new service to run or
authenticate against." With HNSW indexing (since 0.5.0), pgvector
"matches or beats dedicated vector databases at 1M scale." 2026 sources
describe the common adoption pattern as starting with pgvector (already-
have-Postgres) and only evaluating Qdrant if a 500K-2M-vector or
filtering-complexity ceiling is actually hit — this platform has no
measured vector-volume need yet (Risk Register #1).
