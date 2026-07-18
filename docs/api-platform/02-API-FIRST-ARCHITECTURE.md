# API-First Architecture

## API Layers

Five layers, ordered from the caller inward. A request crosses layers
1→4 in order; it never skips a layer, and a Module never accepts a call
that bypasses layers 1–3.

| Layer | Name | Purpose | Owner |
|---|---|---|---|
| 1 | **Edge / Public API Gateway** | Single entry point for every External, Partner, Public, and Admin call. Terminates TLS, authenticates, performs coarse authorization, applies rate limiting, routes. | Public API Gateway (Independent Component, Constitution Section 11) — see `10-API-GATEWAY.md` for the explicit gap: no specific Gateway product is yet ratified. |
| 2 | **Backend-for-Portal / Routing Layer** | Resolves Tenant/Organization/Branch/Data Scope for the authenticated caller and routes to the correct Module contract, consistent with the project's "routing to the right Portal/Dashboard" requirement. | Tenant and Organization Management + Identity and Access (jointly). |
| 3 | **Module Contract Layer** | Each of the 28 Modules exposes its API strictly as defined in `03-API-DOMAIN-INVENTORY.md`. This is where Domain-Driven Design's Bounded Context boundary is enforced in code, not just in documents. | Each Module (Single Adoption Point discipline, mirrored from the Technology Baseline's Owner column). |
| 4 | **Domain / Aggregate Layer** | Aggregates (`TestOrder`, `Specimen`, `TestResult`, ...) enforce their own invariants; this layer is never addressed directly by an API caller — only through Layer 3's contract. | Each Module, internal. |
| 5 | **Anti-Corruption Layer (external Engine boundary)** | Every ratified Engine (Keycloak, OPA, ERPNext, Kill Bill, openIMIS, etc.) is reached only through a translation layer that converts its native model to this platform's domain model, never the reverse. | Each Module that owns an Engine's Single Adoption Point. |

Layers 1–2 are platform-wide and shared; Layers 3–5 are Module-owned
and repeat per Module. This mirrors ADR-0001 (Modular Monolith) and
ADR-0003 (Schema per Module): Modules are internally cohesive and
externally accessed only through their declared contract.

## Request Lifecycle

1. **Client → Edge (Layer 1).** TLS terminated. `Authorization` header
   (OIDC/JWT, see `08-AUTHENTICATION.md`) validated against Keycloak.
   Correlation ID assigned or propagated (`05-API-STANDARDS.md`).
2. **Edge → Coarse AuthZ.** Gateway calls OPA (`09-AUTHORIZATION.md`)
   for a policy decision: is this identity, at this Role, permitted to
   call this endpoint at all? A `deny` short-circuits here — the
   request never reaches a Module.
3. **Edge → Routing (Layer 2).** Tenant/Organization/Branch/Data Scope
   resolved from the validated token's claims and routed to the owning
   Module's Layer-3 contract.
4. **Module boundary (Layer 3) → Fine-grained AuthZ.** The Module
   performs its own OPA check for Data-Scope-level authorization
   (defense in depth — the Edge's `deny` covers endpoint-level access,
   the Module's own check covers *which rows*). This is the
   Backend-Enforced Security requirement (CLAUDE.md Section 14) made
   concrete.
5. **Module → Aggregate (Layer 4).** The Aggregate's own invariants
   apply; a request that violates a domain invariant is rejected here,
   independent of authorization.
6. **Module → External Engine, if applicable (Layer 5).** Only via the
   Anti-Corruption Layer; the Engine's native response never reaches
   the caller unmapped.

## Response Lifecycle

1. **Aggregate → DTO.** Domain objects are mapped to response DTOs
   (`06-NAMING-CONVENTIONS.md`); internal domain fields not part of the
   published contract are never leaked by accident (explicit
   allow-list mapping, not deny-list).
2. **DTO → Data-Scope filter.** Fields and rows are filtered a second
   time at the response boundary against the caller's Data Scope —
   the same defense-in-depth posture as the request path.
3. **DTO → Envelope.** A consistent response envelope (status,
   correlation ID, pagination metadata where applicable) is applied
   (`05-API-STANDARDS.md`).
4. **Envelope → Localization.** Locale-sensitive fields are rendered
   per the caller's `Accept-Language` (ADR-0010, Accepted).
5. **Envelope → Edge → Client.** The Gateway may apply
   protocol-level transformation (e.g., legacy-version compatibility
   shims, `07-VERSIONING.md`) but never business-logic transformation.

## Boundary Rules

- **No direct cross-module database access.** (**Fact**, ADR-0003,
  Accepted — "No direct cross-module database access" is Accepted
  Architecture Principle #14.) A Module that needs another Module's
  data calls its API contract or subscribes to its Domain/Integration
  Events (ADR-0004) — never queries its schema directly.
- **No Engine's native API is exposed to a Portal, Partner, or Public
  consumer directly.** Every external Engine sits behind an
  Anti-Corruption Layer and this platform's own contract.
- **The Edge Gateway holds no business logic.** It authenticates,
  performs coarse authorization, routes, rate-limits, and transforms
  protocol-level concerns only (`10-API-GATEWAY.md`).
- **A Module's Internal API is never reachable through the Edge
  Gateway.** Only External, Partner, Public, and Admin API types
  (`03-API-DOMAIN-INVENTORY.md`) are Edge-routable.
- **Sensitive Operations require Human-in-the-Loop enforcement inside
  the Module layer, not the Gateway.** (`ResultVerified`,
  `ResultReleased`, Break-Glass Access, AI-assisted actions per
  ADR-0007 and CLAUDE.md Section 15.) The Gateway cannot make this
  determination — only the owning Module's domain logic can.

## Layer Responsibilities Summary

| Layer | Does | Does Not Do |
|---|---|---|
| Edge Gateway | AuthN, coarse AuthZ, rate limiting, routing, protocol transformation, correlation ID assignment | Business logic, fine-grained Data Scope filtering, Sensitive Operation gating |
| Routing Layer | Tenant/Org/Branch resolution, Portal/Dashboard routing | Domain validation |
| Module Contract Layer | Publishes the versioned, governed contract; fine-grained AuthZ | Cross-module data access |
| Aggregate Layer | Domain invariants, Sensitive Operation / HITL gating | Direct external exposure |
| Anti-Corruption Layer | Translates Engine-native models to domain models | Ever passing an Engine's native shape through unmodified |
