# API Standards

Every standard below is labeled **Fact** (already Accepted elsewhere
and simply restated here), or **Recommendation** (this Board's proposed
default, not yet an independent ADR, pending API Governance
ratification per `04-API-GOVERNANCE.md`), per CLAUDE.md Section 11's
requirement to separate Facts from Recommendations.

## REST and HTTP

**Recommendation.** REST (resource-oriented, HTTP-method-semantic) is
the default API style for this platform (see `01-API-VISION.md` for
the rationale). HTTP methods carry their standard semantics:

| Method | Use | Idempotent | Safe |
|---|---|---|---|
| `GET` | Retrieve a resource or collection | Yes | Yes |
| `POST` | Create a resource, or invoke a non-idempotent domain action | No | No |
| `PUT` | Replace a resource entirely | Yes | No |
| `PATCH` | Partially update a resource | No (unless designed idempotent) | No |
| `DELETE` | Remove a resource | Yes | No |

A domain action that isn't a pure CRUD verb (e.g., `ResultVerified`,
`ResultReleased`) is modeled as `POST` on a sub-resource or an
action-shaped endpoint (`06-NAMING-CONVENTIONS.md`), never overloaded
onto `PATCH` with a magic field.

## JSON

**Recommendation.** `application/json` is the default request/response
media type. Field names are `camelCase` (see `06`). No API returns
XML unless required by an external standard it must interoperate with
(e.g., a future HL7 v2/ASTM boundary, which stays inside the Device
Integration Gateway's Anti-Corruption Layer and is never the platform's
own external JSON contract).

## Error Model

**Recommendation.** A single, consistent error shape across every API,
modeled on RFC 7807 Problem Details:

```json
{
  "type": "https://platform/errors/validation-failed",
  "title": "Validation failed",
  "status": 422,
  "detail": "specimenId is required",
  "correlationId": "…",
  "errors": [{ "field": "specimenId", "message": "required" }]
}
```

No API invents its own bespoke error envelope. Localized `title`/
`detail` text respects `Accept-Language` (ADR-0010, Accepted).

## Pagination

**Recommendation.** Cursor-based pagination (`?cursor=...&limit=...`)
is the default for any collection that can grow unbounded (Test
Orders, Specimens, Audit Events, Notifications). Offset-based
pagination (`?page=...&pageSize=...`) is acceptable only for small,
bounded Admin lists (e.g., a Tenant's Branch list). Every paginated
response includes a `nextCursor` (or `null` at the end) — never a
bare array with no continuation metadata.

## Filtering and Sorting

**Recommendation.** Filtering via explicit query parameters matching
resource field names (`?status=verified`), not a generic query
language, to keep every Module's filterable fields deliberate and
reviewable at the Quality Gate step. Sorting via `?sort=fieldName` or
`?sort=-fieldName` for descending. Both are additive (non-breaking) to
introduce later.

## Localization

**Fact.** ADR-0010 (Arabic/English and Localization-First) is
Accepted. Every API honors `Accept-Language` for localized field
content and returns locale-aware formatting for dates/numbers where
the response includes human-readable text. Machine-readable fields
(IDs, enums, ISO-formatted timestamps) are never localized.

## Time Zones

**Recommendation.** All timestamps are transmitted in UTC, ISO 8601
(`2026-07-18T09:00:00Z`), on the wire. Tenant-local display conversion
happens at the client/Portal layer, consistent with Accepted
Architecture Principle #17 (Multi-Tenant, Multi-Organization,
Multi-Branch — which the reuse program's own SaaS Discovery treats as
implying multi-timezone support, though no ADR pins the exact
conversion mechanism).

## UUIDs

**Recommendation.** New resource identifiers use UUIDv7
(time-orderable) rather than UUIDv4, to keep database index locality
reasonable at scale. This is a Recommendation only — no ADR has
evaluated identifier strategy, and it does not conflict with any
Accepted decision.

## Correlation IDs

**Recommendation.** Every request carries (or is assigned, if absent)
an `X-Correlation-Id` header, propagated through every layer in
`02-API-FIRST-ARCHITECTURE.md`'s request lifecycle and included in
every error response and every Audit Event (Audit and Compliance).
Full distributed tracing is explicitly Part 2 (Observability) — this
Recommendation establishes only the identifier discipline that
Observability will later build on, not the tracing infrastructure
itself.

## Idempotency

**Recommendation.** Any unsafe operation touching a financial or
clinical write (Billing charges, Payments, `ResultVerified`,
`ResultReleased`, Break-Glass Access) requires an `Idempotency-Key`
header; a repeated call with the same key returns the original result
rather than repeating the effect. This directly supports the Sensitive
Operation / Human-in-the-Loop discipline (CLAUDE.md Section 15) by
ensuring a retried request cannot silently duplicate a clinical or
financial action.

## Status Codes

**Recommendation**, standard HTTP semantics applied consistently:

| Code | Meaning | Typical Use |
|---|---|---|
| 200 | OK | Successful `GET`/`PATCH`/`PUT`/action |
| 201 | Created | Successful `POST` creating a resource |
| 202 | Accepted | Async operation accepted (e.g., a device-import batch) |
| 204 | No Content | Successful `DELETE` |
| 400 | Bad Request | Malformed request |
| 401 | Unauthorized | Missing/invalid authentication |
| 403 | Forbidden | Authenticated but not authorized (RBAC/ABAC/OPA deny) |
| 404 | Not Found | Resource does not exist or caller has no Data Scope to see it (never distinguish the two in the response body, to avoid enumeration leakage) |
| 409 | Conflict | Optimistic-lock/version conflict on an Aggregate |
| 422 | Unprocessable Entity | Domain validation failure |
| 429 | Too Many Requests | Rate limit exceeded (`13-RATE-LIMITING.md`) |
| 500 | Internal Server Error | Unhandled fault |
| 503 | Service Unavailable | Downstream Engine/Independent Component unavailable |
