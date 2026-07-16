# Architecture Review — Semantic Search

pgvector directly reuses Module 2's PostgreSQL + RLS decision — vectors
inherit the same tenant-isolation guarantee for free, no separate
multi-tenancy design needed for a second database. This is a strong,
evidence-based reason to prefer pgvector specifically for *this*
platform over a generically "faster" dedicated vector database.
