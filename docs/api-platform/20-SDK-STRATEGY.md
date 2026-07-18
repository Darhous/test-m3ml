# SDK Strategy

## Disambiguation — Not a Contradiction of Part 1

**Fact, stated explicitly to prevent a false contradiction:**
`docs/architecture-review/05-SDK-BASELINE.md` (EARB phase) found **0
third-party SDKs ratified** — meaning the platform does not
independently adopt an external vendor's client library (WhatsApp BSP
SDK, a payment-gateway SDK) as a first-class Technology Baseline
dependency; those integrations are wrapped behind this platform's own
abstraction instead (e.g., `payment-gateway-abstraction`,
Omnipay-pattern, R5 in the Technology Baseline).

**This document is about the opposite direction: SDKs this platform
itself produces**, for developers consuming *this platform's* API
(`01-API-VISION.md`'s Developer Experience Vision). These are two
unrelated questions — "which vendor SDKs do we consume" (EARB, closed,
0 ratified) versus "do we publish our own SDKs for our API" (this
document, Part 2). No prior finding is revisited or contradicted.

## SDK Architecture

**Recommendation.** Every officially published SDK is a thin,
generated client wrapping the Published OpenAPI contracts
(`17-OPENAPI-GOVERNANCE.md`) — it contains no independent business
logic, no bypass of the Edge Gateway, and no embedded credentials. An
SDK's authentication helper implements the OAuth2 grants already
defined in `08-AUTHENTICATION.md` (Authorization Code + PKCE for
end-user-facing SDK usage, Client Credentials for a Partner's
server-to-server SDK usage) — it does not invent a parallel auth
scheme.

## Generation

**Recommendation**, tool selection deferred to `31-ENTERPRISE-PRODUCT-
DECISIONS.md`. SDKs are generated from the same Published OpenAPI
document that drives `22-DEVELOPER-PORTAL.md`'s Interactive Docs —
never hand-written independently, which would let the SDK and the
contract drift. A contract change that breaks SDK generation is itself
a signal the change violates `16-CONTRACT-FIRST.md`'s Backward
Compatibility verification and should not have passed that gate.

## Supported Languages

**This Board does not fix a specific language list.** No
`.claude/context/` artifact or user instruction states which languages
the platform's Partner/Public developer base actually needs — asserting
one (e.g., "Python, JavaScript, PHP") would be a guess this phase's
No-Guessing Rule forbids. What is fixed instead: language selection is
demand-driven (informed by which Partners/consumers actually request
integration, once Partner APIs in `21-INTEGRATIONS.md` have real
counterparties) and the generation pipeline (above) is chosen partly
*because* it supports adding a new target language without a
contract-level change — deferring the language-list decision does not
block the architecture.

## Packaging

**Recommendation.** Each SDK is published to the packaging ecosystem
native to its language (e.g., a package registry per language
runtime), versioned independently per language but derived from the
same contract version (`07-VERSIONING.md`) — an SDK's major version
tracks its underlying API contract's major version, so a consumer can
reason about compatibility without reading two separate changelogs.

## Versioning and Release Strategy

SDK versioning inherits `07-VERSIONING.md`'s Compatibility and
Deprecation Policy directly — an SDK for API `/v1` is deprecated on
the same timeline as `/v1` itself, not a separately negotiated one.
Release channels mirror `29-LIFECYCLE.md`'s platform-wide release
channel model (see that document) rather than each SDK inventing its
own alpha/beta/stable convention.

## Maintenance

**Recommendation.** An SDK is a generated artifact, not hand-maintained
code — its maintenance burden is the maintenance burden of the
underlying OpenAPI contract plus the generation pipeline itself, not N
independent codebases growing apart. This is the direct architectural
reason generation (not hand-authoring) is required, not merely
preferred: hand-maintained SDKs across multiple languages would
multiply this platform's maintenance surface by the number of
languages supported, with no corresponding benefit the generated
approach doesn't already provide.

## Dependency on Other Documents

- Requires `16-CONTRACT-FIRST.md`'s OpenAPI-as-source-of-truth
  discipline to already be in force — an SDK generated from a
  hand-drifted or informally documented API would inherit that drift.
- Requires `21-INTEGRATIONS.md`'s Partner Certification process to
  determine which Partners' target languages actually justify
  investment.
- Product/tool selection: `31-ENTERPRISE-PRODUCT-DECISIONS.md`.
