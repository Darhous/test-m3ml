# API Security

Produced using the `stride-analysis-patterns` Skill's methodology,
applied to the API layers defined in `02-API-FIRST-ARCHITECTURE.md`.
Full Observability/incident-response tooling is Part 2 scope; this
document defines the security *architecture*, not the monitoring
*tooling*.

## OWASP API Security Top 10 — Platform Mapping

| # | Threat | Platform Control |
|---|---|---|
| API1 | Broken Object Level Authorization | Module-boundary ABAC/Data-Scope PEP (`09-AUTHORIZATION.md`) checks row-level ownership on every request — never inferred from a client-supplied ID alone. |
| API2 | Broken Authentication | Keycloak-issued OIDC/JWT, short-lived access tokens, rotating refresh tokens (`08-AUTHENTICATION.md`); no Module implements its own auth. |
| API3 | Broken Object Property Level Authorization | DTO mapping is explicit allow-list, not deny-list (`02-API-FIRST-ARCHITECTURE.md` Response Lifecycle); Role/Policy govern which fields appear, not just which resources. |
| API4 | Unrestricted Resource Consumption | Rate limiting and quotas (`13-RATE-LIMITING.md`) at the Gateway. |
| API5 | Broken Function Level Authorization | OPA RBAC decision per endpoint at the Gateway (`09-AUTHORIZATION.md`); Admin-classified endpoints (`03-API-DOMAIN-INVENTORY.md`) require an elevated Role, checked independently of resource-level checks. |
| API6 | Unrestricted Access to Sensitive Business Flows | Human-in-the-Loop gating at the Aggregate layer for Sensitive Operations — `ResultVerified`, `ResultReleased`, Break-Glass Access, AI-assisted actions (ADR-0007, CLAUDE.md Section 15) — enforced in domain logic, not bypassable via the Gateway. |
| API7 | Server-Side Request Forgery | Every external Engine call passes through a Module-owned Anti-Corruption Layer (`02-API-FIRST-ARCHITECTURE.md` Layer 5); no Module accepts a caller-supplied URL and fetches it directly. |
| API8 | Security Misconfiguration | Quality Gates (`04-API-GOVERNANCE.md`) required before Publish; no API ships without passing this document's checklist. |
| API9 | Improper Inventory Management | `03-API-DOMAIN-INVENTORY.md` is the canonical, Board-maintained inventory of every API surface across all 28 Modules — the direct structural answer to this threat category. |
| API10 | Unsafe Consumption of APIs | Every AGPL/unconfirmed-license Engine (Cal.com, Atlas CMMS, openIMIS, Frappe Helpdesk, Frappe CRM, Novu, Documenso) is wrapped behind an Anti-Corruption Layer specifically so a change in that Engine's own API surface cannot propagate unfiltered into this platform's contract; see `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` for the legal dimension of the same boundary. |

## STRIDE Threat Model

Applied at the Gateway/Module boundary (`02-API-FIRST-ARCHITECTURE.md`'s
Layers 1–3), per the `stride-analysis-patterns` Skill:

| Category | Threat | Control |
|---|---|---|
| **Spoofing** | An attacker impersonates a user or service identity | OIDC/JWT for human identities; mTLS-backed Client Credentials for service/Partner identities (`08-AUTHENTICATION.md`) |
| **Tampering** | Request/response data is modified in transit | TLS everywhere (transport, below); request signing recommended for Partner APIs where the counterpart is outside this platform's own network trust boundary |
| **Repudiation** | A caller denies having performed a Sensitive Operation | immudb-backed Audit and Compliance trail (Technology Baseline E4) for every Sensitive Operation and every Break-Glass invocation, matching Full Auditability (Accepted Architecture Principle #10) |
| **Information Disclosure** | A caller sees data outside their Data Scope | Two-PEP defense-in-depth (`09-AUTHORIZATION.md`) plus response-time Data-Scope filtering (`02-API-FIRST-ARCHITECTURE.md`); `404`, not `403`, on out-of-scope resource IDs to avoid confirming existence (`05-API-STANDARDS.md`) |
| **Denial of Service** | The API is overwhelmed | Rate limiting and burst controls (`13-RATE-LIMITING.md`), Gateway circuit-breaking (`10-API-GATEWAY.md`) |
| **Elevation of Privilege** | A caller gains access beyond their Role/Policy | OPA policy enforcement at both PEPs; Break-Glass is its own explicit, separately-audited path, never a silent policy exception (`09-AUTHORIZATION.md`) |

## Encryption

**Recommendation.** TLS 1.2 or higher in transit, platform-wide, for
every API type. At-rest encryption follows from the Hybrid Tenant
Isolation model's dedicated-database tier for large/regulated tenants
(ADR-0005, Accepted) — this document does not re-specify at-rest
mechanics already covered by that ADR.

## Transport Security

**Recommendation.** mTLS for service-to-service calls (Module-to-Module
where they cross a process boundary, and any Partner Integration API)
— consistent with Zero Trust, since network position alone (e.g.,
"inside the VPC") is never treated as sufficient authentication.

## Validation

Schema validation occurs at both the Gateway (structural/type-level,
where a specific Gateway product is eventually chosen — `10`) and the
Module boundary (domain-level, always). Unknown fields in a request are
rejected, not silently ignored, to prevent silent contract drift.

## Replay Protection

`Idempotency-Key` (`05-API-STANDARDS.md`) prevents duplicate effects
from a retried unsafe request. Short-lived access tokens
(`08-AUTHENTICATION.md`) bound the window in which a captured token is
useful. Nonce-based replay protection for asynchronous, webhook-style
callbacks is explicitly deferred — Webhooks are Part 2 scope.

## Security Headers

**Recommendation**, standard set applied at the Gateway/Module response
path: `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`,
`Content-Security-Policy` (for any Module serving HTML, e.g. Document
Management's e-signature flows), `Referrer-Policy`. No API response
includes a header that leaks internal infrastructure details (server
version, internal hostnames).
