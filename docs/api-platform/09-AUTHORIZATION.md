# Authorization

## RBAC

**Fact.** Role-Based Access Control is the coarse-grained layer of
ADR-0008 ("Unified Login and Policy-Based Access", Accepted). A `Role`
is defined in `.claude/context/glossary.md`'s Accepted vocabulary as "a
functional classification that determines a user's general access
type." Roles gate *which endpoints* an identity may call at all — the
Edge Gateway's coarse authorization step in
`02-API-FIRST-ARCHITECTURE.md`.

## ABAC

**Fact.** Attribute-Based Access Control is the fine-grained layer of
the same ADR-0008 decision. A `Policy` (Accepted glossary definition:
"a rule determining how Permissions apply given a context — Data
Scope, Organization, Branch...") governs *which rows/fields* an
already-Role-permitted identity may see or act on. This is the Module
boundary's own authorization check in `02-API-FIRST-ARCHITECTURE.md`'s
request lifecycle — deliberately separate from the Edge Gateway's RBAC
check, so a defect in one layer does not silently become a full
authorization bypass.

## Permission Model

```
Role      → coarse: "can this identity call this endpoint at all?"
Policy    → fine:   "given Tenant/Organization/Branch/Data Scope,
                      which specific resources can this identity see
                      or act on?"
Permission → the atomic, granular grant (Accepted glossary definition)
             that a Role bundles and a Policy contextualizes.
```

This three-part model is not new — it is the Accepted glossary
vocabulary (`Role`, `Permission`, `Policy`, `Data Scope`) applied
directly to API design, not a reinterpretation of it.

## OPA Integration

**Fact.** Open Policy Agent (Technology Baseline E2, Apache-2.0,
ADR-0008) is the platform's policy decision point. It is, per the
Enterprise Adoption Review's own finding
(`docs/architecture-review/10-ADR-REVIEW.md`), the single most-reused
Engine in the entire 28-Module program (8 Modules), which this Board
treats as strong existing evidence that OPA's policy model scales
cleanly to the API layer, not as a new finding this Board is
independently re-verifying.

Every API call, at both the Edge Gateway (RBAC-level decision) and the
Module boundary (ABAC/Data-Scope-level decision), issues a decision
query to OPA. OPA decisions are: (a) centrally authored and versioned
as policy bundles (per the Technology Baseline's own Upgrade Policy for
E2 — "policy bundles versioned independently" of the OPA engine
itself), and (b) never hardcoded per-Module as an if/else authorization
check, which would defeat the purpose of a shared policy engine and
reintroduce the inconsistency ADR-0008 was written to prevent.

## Policy Enforcement Points (PEP)

Two PEPs, by design (defense in depth, matching
`02-API-FIRST-ARCHITECTURE.md`'s two-step authorization in the request
lifecycle):

1. **Edge Gateway PEP** — coarse, Role-level. A `deny` here means the
   request never reaches a Module at all.
2. **Module boundary PEP** — fine, Data-Scope-level. A `deny` here
   means the caller was permitted to call the endpoint but not to see
   or act on this specific resource/row/field.

Neither PEP substitutes for the other. A Module must never assume the
Edge Gateway's `allow` already covers Data-Scope correctness — this is
the direct, concrete meaning of CLAUDE.md Section 14 ("Authorization
and access control must be enforced in the backend, not only in the
UI") extended one layer further: not only in the UI, and not only at
the Gateway either.

## Break-Glass Access

**Fact**, Accepted glossary definition, reused verbatim: "exceptional
emergency access, time-limited, justified, and fully audited, that
bypasses the normal authorization path." At the API layer, Break-Glass
is modeled as its own explicit, separately-logged authorization path —
never a silent OPA policy exception indistinguishable from ordinary
access in the audit trail. Every Break-Glass invocation is written to
Audit and Compliance's immudb-backed store (Technology Baseline E4)
with full justification metadata, consistent with Full Auditability
(Accepted Architecture Principle #10) and with `11-RISKS.md`'s R-04/R-07
legal-review discipline being extended, not bypassed, by an emergency
path.
