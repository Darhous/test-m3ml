# Integration Options — Authentication

## Recommended Pattern: Anti-Corruption Layer over an OIDC Contract

Consistent with Constitution Section 8 (One Owning Module Per Bounded
Context) and Section 9/10 (Core Platform dependency rules): the platform's
own Identity and Access Bounded Context (Wave 9, Context 27) does **not**
become Keycloak — it becomes a thin, owned Anti-Corruption Layer that
speaks OIDC/OAuth2 to Keycloak and exposes the platform's own
Ubiquitous-Language-correct contract (per Wave 8's glossary work) to
every other Bounded Context. No other Module should call Keycloak's Admin
REST API directly — only the Identity and Access Module does, exactly
matching Constitution Section 7's Open Host Service + Published Language
guidance already applied elsewhere in Discovery (e.g., ADR 0012's
Organization/Branch reference-data decision).

## Integration Options Considered

1. **Direct embed (Keycloak as a Java library inside the platform's own
   process).** Rejected — Keycloak is designed and overwhelmingly deployed
   as a separately-run service; embedding fights the grain of the
   project and would forfeit its independent upgrade path.
2. **Engine + Adapter (Keycloak as a separately-deployed service, platform
   integrates via OIDC/OAuth2 + Admin REST API through an owned adapter).**
   **Selected.** Matches Constitution Section 11's Independent Component
   pattern (already used for Notification Service and Device Integration
   Gateway) even though Identity and Access is Platform Kernel, not an
   Independent Component in the Constitution's specific sense — the
   integration *shape* (adapter, not embed) is the same discipline.
3. **Full replacement build.** Rejected per `08-build-vs-buy.md`.

## Data Flow

Keycloak issues signed JWTs (OIDC ID Token + Access Token) → platform's
Identity and Access adapter validates signature/claims → adapter emits
the platform's own `UserAuthenticated` Domain Event (Wave 5 event
vocabulary) → downstream Modules consume the platform's event, never
Keycloak's own internal event format directly.

## Multi-Tenancy Integration Note

Keycloak's Organizations feature (stabilized v26) is a **candidate**
mechanism for `open-questions.md` #15 (shared-tier partitioning), not a
decision — this Feature's adoption does not itself resolve that Open
Question; it narrows the *tooling* available once the question is
answered (see `12-risk-analysis.md`).
