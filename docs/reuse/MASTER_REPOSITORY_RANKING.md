# Master Repository Ranking

Enterprise-weighted ranking (not GitHub-stars-based) of every candidate,
grouped by Feature. Full per-dimension scoring lives in each Feature's
`03-candidate-repositories.md` and `05-architecture-review.md`. This file
is the cross-Feature leaderboard view.

**Scoring dimensions and weights:** see `MASTER_COMPARISON_MATRIX.md`
header — identical model applied everywhere for comparability.

| Module | Feature | Rank | Candidate | Weighted Score | One-Line Why |
|---|---|---|---|---|---|
| Identity and Access | authentication | 1 | Keycloak | 4.6 | CNCF governance + explicit regulated-industry adoption evidence + cleanest license |
| Identity and Access | authentication | 2 | Authentik | 3.5 | Best admin UX, thinner regulated-industry evidence |
| Identity and Access | authentication | 2 | Ory | 3.5 | Most flexible, most integration burden |
| Identity and Access | authentication | 4 | Zitadel | 3.3 | Strong architecture, AGPL licensing complication |
| Identity and Access | authorization-rbac-abac | 1 | OPA | 4.7 | CNCF Graduated, purpose-built for the 8-dimension Policy Model shape |
| Identity and Access | authorization-rbac-abac | 2 | Casbin | 4.1 | Simpler, close second, credible fallback |
| Identity and Access | authorization-rbac-abac | 3 | Keycloak Authorization Services | 3.6 | Avoids a second engine, but weakest architectural fit |
