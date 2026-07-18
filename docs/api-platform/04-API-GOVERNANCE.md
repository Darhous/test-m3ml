# API Governance

## Ownership

Every API surface has exactly one owning Module, mirroring the Single
Adoption Point discipline already established and frozen in
`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`'s Owner column.
An API is never jointly owned by two Modules; where two Modules
collaborate on a workflow (e.g., Billing and Insurance and Corporate
Contracts), each still owns and versions its own contract independently
— collaboration happens through calls or events, not shared ownership.
(**Recommendation**, extending an existing Fact-level pattern to a new
domain.)

## Governance Body

The Architecture Review Board function already Accepted in
`docs/constitution/PROJECT-CONSTITUTION.md` Section 59 is the standing
governance body for API contracts of type External, Partner, Admin, or
Integration (per `03-API-DOMAIN-INVENTORY.md`'s classification).
Internal APIs are reviewed within the owning Module team but must still
respect the boundary rules in `02-API-FIRST-ARCHITECTURE.md`. This
Board does not create a new governance body — it assigns API review
into the existing one. (**Recommendation**, reusing rather than
inventing a governance structure, consistent with this phase's Do-Not
list against inventing new organizational scope.)

## Review Process

1. **Contract draft.** The owning Module drafts the contract
   (resource shape, operations, error model) before writing
   implementation code — Contract-First.
2. **Module Owner review.** Checked against `05-API-STANDARDS.md` and
   `06-NAMING-CONVENTIONS.md`.
3. **Cross-Module impact check.** Checked against the Bounded Context
   Map (ADR-0012, Proposed — used as working structure per its own
   status) to confirm no boundary violation and no unintended
   dependency on another Module's internal contract.
4. **Architecture Review Board approval.** Required for any API
   classified External, Partner, Admin, or Integration in
   `03-API-DOMAIN-INVENTORY.md`. Internal-only APIs do not require
   Board approval but do require the Module Owner review step.
5. **Published.** Only after all prior steps pass.

## Approval Workflow

```
Draft → Module Owner Review → Cross-Module Impact Check
      → [External/Partner/Admin/Integration only] Architecture Review Board
      → Published
```

A Partner or Public-adjacent contract additionally requires the
license/legal posture of any Engine it exposes to be checked against
`docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` before
Publication — e.g., an Insurance and Corporate Contracts Partner API
built on openIMIS (AGPL-3.0, `Requires Legal Verification`) cannot be
finalized until that checklist clears, consistent with
`docs/architecture-review/13-READINESS-FOR-API-STRATEGY.md`'s own
blocking-item finding.

## Breaking Change Policy

- A **breaking change** is any change that would cause an existing,
  correctly-implemented consumer to fail or receive semantically
  different data: removing a field, renaming a field, changing a
  field's type or meaning, removing an endpoint, changing an error
  code's meaning, or tightening a validation rule.
- A **non-breaking change** is additive: a new optional field, a new
  endpoint, a new optional query parameter, a new enum value where the
  consumer contract explicitly documents forward-compatibility for
  enums.
- No breaking change ships without a new major version
  (`07-VERSIONING.md`) and a published deprecation notice on the
  version it replaces.

## Lifecycle

APIs follow the same four-stage lifecycle discipline already
established for ADRs in this project (`architecture-decision-records`
Skill, reused deliberately for consistency rather than inventing a
parallel scheme):

```
Draft → Published → Deprecated → Retired
```

- **Draft**: under active design/review, not callable by any consumer
  outside the owning Module's own testing.
- **Published**: the contract is live and consumers may depend on it.
- **Deprecated**: still callable, but a retirement date is published
  and dual-version support is active (`07-VERSIONING.md`).
- **Retired**: no longer callable; the version returns a `410 Gone`
  with a pointer to its replacement.

## Quality Gates

An API cannot move from Draft to Published without passing every gate
below — mirroring the Quality Gates discipline Accepted in Constitution
Section 52, applied here to the API surface specifically:

| Gate | Checked Against |
|---|---|
| Naming conformance | `06-NAMING-CONVENTIONS.md` |
| Standards conformance (error model, pagination, status codes, etc.) | `05-API-STANDARDS.md` |
| Versioning declared | `07-VERSIONING.md` |
| AuthN/AuthZ model declared | `08-AUTHENTICATION.md`, `09-AUTHORIZATION.md` |
| Security review (OWASP API Top 10 + STRIDE) | `11-API-SECURITY.md` |
| Multi-tenancy isolation check | `14-MULTI-TENANCY.md` |
| Rate-limiting tier assigned | `13-RATE-LIMITING.md` |
| License/legal posture clear (if the API exposes an AGPL/unconfirmed-license Engine) | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` |

No gate may be waived by an individual Module team — the same
non-negotiable discipline the Technology Baseline freeze already
established (`docs/architecture-review/12-DECISION-FREEZE.md`).
