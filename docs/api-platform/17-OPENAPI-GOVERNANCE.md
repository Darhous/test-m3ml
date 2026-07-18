# OpenAPI Governance

**Scope note:** Governs the *notation and documentation standards* for
REST contracts specifically. `16-CONTRACT-FIRST.md` governs the
*process*; this document governs the *artifact format*. Event contracts
use AsyncAPI, covered separately in `18-ASYNCAPI-EVENTS.md`.

## OpenAPI Standards

**Recommendation.** OpenAPI 3.1.x is the mandatory notation for every
REST contract (`03-API-DOMAIN-INVENTORY.md`'s External, Partner,
Admin, and Integration APIs; Internal APIs are also encouraged to use
it for consistency, though enforcement is lighter given they never
cross the Edge Gateway). 3.1.x is chosen over 3.0.x because it is
fully JSON Schema-compatible, which matters directly for this
platform's DTO reuse rules (`16`'s Schema Governance) and for
`20-SDK-STRATEGY.md`'s generation pipeline, which works materially
better against full JSON Schema. No API ships a Swagger 2.0 (OpenAPI
2.0) document — that format is legacy and lacks the `oneOf`/`anyOf`
composition this platform's polymorphic resources (e.g., a `TestOrder`
whose specimen-handling fields vary by test type) require.

## Reusable Components

Every OpenAPI document defines its schemas, parameters, responses, and
security schemes under `components/`, referenced via `$ref` — never
inlined redundantly across operations. This is `16-CONTRACT-FIRST.md`'s
Schema Governance rule made OpenAPI-concrete. Standard reusable
components every Module's contract must define once and reuse:

| Component | Purpose |
|---|---|
| `ErrorResponse` | The RFC-7807-shaped error envelope (`05-API-STANDARDS.md`) |
| `PaginatedResponse` | Cursor-based pagination envelope (`05-API-STANDARDS.md`) |
| `CorrelationIdHeader`, `TenantIdHeader`, `IdempotencyKeyHeader` | The standard headers (`06-NAMING-CONVENTIONS.md`) |
| `BearerAuth` security scheme | OIDC/JWT bearer token (`08-AUTHENTICATION.md`) |

These four are platform-wide reusable components every Module's
contract references identically — the one deliberate exception to
"schemas are never shared across Module contracts" in `16`, because
these are cross-cutting infrastructure shapes, not domain models, and
sharing them is what keeps every Module's contract mechanically
consistent.

## Validation

**Recommendation.** Every OpenAPI document is validated at two levels
before it can pass the Draft → Published Quality Gate
(`04-API-GOVERNANCE.md`):

1. **Structural validation** — is this a syntactically valid OpenAPI
   3.1 document (automated, tool-enforced, not a matter of reviewer
   judgment).
2. **Convention validation** — does it conform to
   `06-NAMING-CONVENTIONS.md` and this document's Reusable Components
   requirement (automated linting against a platform-specific ruleset,
   not manual review for every rule).

Runtime request/response validation against the Published contract
happens at the Module boundary (`02-API-FIRST-ARCHITECTURE.md`) — a
request that does not conform to the Published schema is rejected with
`400`/`422`, not silently accepted and left to downstream code to
discover the mismatch.

## Documentation Standards

Every operation, parameter, and schema field carries a human-readable
`description` — an OpenAPI document with types but no prose is
incomplete and fails the Documentation Quality Gate. Descriptions are
written for the audience `22-DEVELOPER-PORTAL.md`'s Interactive Docs
will actually render them to: a Module team member unfamiliar with
this specific Module, not just the contract's own author. Every
`description` field is a localization candidate (`Accept-Language`,
ADR-0010) for external-facing (Partner/Public-adjacent) documentation
— see `22`'s Interactive Docs section for how this is rendered;
authoring the source description in English is acceptable, with
translation as a Developer Portal rendering concern, not an OpenAPI
authoring requirement (avoids requiring every Module author to
maintain bilingual OpenAPI source by hand).

## Version Governance

The OpenAPI document's own `info.version` field tracks the contract's
major version from `07-VERSIONING.md` (e.g., `1.0.0` for `/v1`, bumping
the major segment only on a breaking change per that document's
Compatibility Policy — minor/patch segments may move freely on
non-breaking additions, giving finer-grained change tracking than the
URL path alone exposes). The OpenAPI document is retained for every
version still in the Published or Deprecated lifecycle stage
(`04-API-GOVERNANCE.md`) — a Retired version's document is archived,
not deleted, so `23-API-CATALOG.md`'s historical record stays intact.
