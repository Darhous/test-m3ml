# Global Search Log — Authorization (RBAC/ABAC)

## Query Run

`Open Policy Agent OPA vs Casbin vs OpenFGA fine-grained authorization
healthcare 2026`

## Landscape Notes

Three genuinely distinct architectural families found, not competing
head-to-head but suited to different problem shapes:
- **Policy-as-code engines (ABAC/RBAC):** Open Policy Agent (OPA), Cerbos.
- **Embedded authorization libraries:** Casbin (supports ACL, RBAC, ABAC,
  ReBAC across many languages, in-process, no separate service to run).
- **Relationship-based (Zanzibar-style) engines:** OpenFGA (CNCF-governed),
  SpiceDB, Ory Keto.

## Fit Assessment Against the Policy Model's Actual Shape

The Configurable Result Verification Policy Model is fundamentally
**attribute/context-driven** (org type, analysis type, risk, specialty,
branch, country policy, emergency override) — this is ABAC/policy-as-code
territory, not a relationship graph (ReBAC) problem. This narrows the
field to **OPA and Casbin** as the credible candidates; OpenFGA/SpiceDB/
Keto are not carried forward as primary candidates (not because they are
bad, but because their core strength — deep relationship graphs, e.g.
"who can see documents shared transitively through a folder hierarchy" —
does not match this Feature's actual requirement shape).

## Candidates Carried Forward

Open Policy Agent (OPA) and Casbin, evaluated alongside Keycloak's own
built-in Authorization Services (fine-grained permission extension) as a
third "don't add a new engine at all" option.
