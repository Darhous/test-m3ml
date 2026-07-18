# Naming Conventions

**All naming below is a Recommendation** pending API Governance
ratification (`04-API-GOVERNANCE.md`'s Quality Gates), except where a
name is already Accepted elsewhere (Domain Events, marked Fact below).
The governing discipline throughout is the `domain-driven-design`
Skill's Ubiquitous Language principle: **a name that a domain expert
cannot recognize is treated as a modeling defect, not a style
preference** — and this platform already has a documented Ubiquitous
Language in `.claude/context/glossary.md` that naming must draw from,
not reinvent.

## Endpoints

- Plural nouns for collections, kebab-case path segments:
  `/test-orders`, `/specimens`, `/test-results`, not `/testOrder`,
  `/get-test-order`, or `/TestOrders`.
- Resource hierarchy reflects Aggregate ownership, not database joins:
  `/test-orders/{id}/specimens` is valid only if `Specimen` is
  genuinely subordinate to `TestOrder` in the domain model — if the
  reuse program's aggregate boundaries say otherwise
  (`.claude/context/glossary.md`'s Discovery Phase 05 candidate
  aggregates lists `Specimen` as its own Aggregate Root), the
  hierarchy must not imply a false containment.
- Actions that are not pure CRUD are modeled as a `POST` on a
  sub-resource, verb-shaped and past-tense-adjacent to match the
  domain event it triggers: `POST /test-results/{id}/verify` (which
  raises `ResultVerified`), not `PATCH /test-results/{id}` with a
  hidden status-change side effect.

## Resources

Resource names are drawn directly from `.claude/context/glossary.md`'s
Ubiquitous Language — never invented technical synonyms. Per Gap
Closure Wave 8's disambiguation work (already done, cited not
repeated), several near-synonyms are **Forbidden** as resource names
because the glossary already assigns them to a specific, different
concept: do not use `Order`, `Request`, `Booking`, `Sample`, `Analysis`,
`Report`, or `Approval` as a resource name where `TestOrder`,
`Encounter`, `Specimen`, `Test`, `DiagnosticReport`, or `ResultVerified`
is the glossary-correct term. This is a direct application of the
`domain-driven-design` Skill's naming-smell diagnostic.

## DTOs

Suffix convention: `{Resource}Request` (input), `{Resource}Response`
(full output), `{Resource}Summary` (list-item/abbreviated output). E.g.
`TestOrderRequest`, `TestOrderResponse`, `TestOrderSummary`. A DTO name
never uses `Manager`, `Helper`, `Processor`, `Data`, or `Info` as a
suffix — these are the exact naming smells the `domain-driven-design`
Skill flags as hiding domain logic from the people who could validate
it.

## Events

**Fact**, not a new Recommendation: Domain Event names are already
established in `.claude/context/glossary.md` (Gap Closure Wave 3/8,
Discovery Phase 03) and are reused verbatim, never renamed for API
purposes: `TestOrdered`, `SpecimenCollected`, `SpecimenAccessioned`,
`SpecimenRejected`, `ResultVerified`, `ResultReleased`,
`ClaimAdjudicated`. Past tense, matching the `domain-driven-design`
Skill's Domain Events pattern (a fact that has already happened).
Integration Events crossing a Module boundary use the same name as the
originating Domain Event — no separate "integration name" is invented,
to avoid the same concept acquiring two names.

## Parameters

- Query parameters: `camelCase` (`?sortBy=createdAt`, not
  `?sort_by=created_at`), for consistency with the JSON body casing.
- Path parameters: singular resource identifier (`{testOrderId}`, not
  `{id}` when ambiguity is possible across nested resources).

## Headers

Standard platform headers, consistent across every Module's API:

| Header | Purpose |
|---|---|
| `X-Tenant-Id` | Explicit tenant context (defense in depth alongside token claims — see `14-MULTI-TENANCY.md`) |
| `X-Correlation-Id` | Request tracing (`05-API-STANDARDS.md`) |
| `X-Idempotency-Key` | Idempotent replay protection for unsafe operations (`05-API-STANDARDS.md`, `11-API-SECURITY.md`) |
| `Accept-Language` | Localization (ADR-0010) |
| `Authorization` | Bearer JWT (`08-AUTHENTICATION.md`) |

## Packages and Namespaces

Code and contract namespaces mirror the 28-Module Catalog exactly
(`.claude/context/module-catalog.md`, `docs/reuse/` directory
structure) — no invented sub-namespacing beyond what those already
define, and no namespace spans two Modules. This keeps the API
namespace and the Schema-per-Module boundary (ADR-0003, Accepted)
mechanically aligned, so a namespace violation is also, by
construction, a schema-boundary violation and easy to catch at review.
