# 0008: Unified Login and Policy-Based Access

## Status

Accepted

## Context

The platform serves multiple client surfaces (Unified Web Platform, Patient
App, Sample Collector/Home Visit App) and multiple user types (patients,
doctors, laboratory staff, organization/platform administrators, finance/
inventory teams, insurance users, suppliers, device integration teams,
support teams, security/compliance teams — `stakeholders.md`), each needing
to reach the right Portal/Dashboard with the right access. The vision
explicitly requires "Unified Login" and routing by Role, Permissions, Data
Scope, Organization, and Branch (`vision.md`) — and the platform must never
rely on UI hiding as an authorization control (explicit user rule).

## Decision

The platform uses a **single, unified authentication entry point** (Unified
Login) for all user types across all clients, backed by a **shared Backend
Platform**. Authorization is **Backend-Enforced** and **Policy-Based**:
every state-changing and sensitive read operation is authorized server-side
using Role, Permissions, Policy, Data Scope, Organization, Branch, Resource
Ownership, and Consent. Least Privilege and Deny by Default apply. Sensitive
operations require elevated controls; emergency Break-Glass access is
exceptional, time-limited, justified, and fully audited.

## Alternatives Considered

- **Separate login/identity systems per client surface (Web, Patient App,
  Collector App).** Rejected: directly contradicts the explicit Unified
  Login requirement, and multiplies the number of places authorization
  logic must be kept consistent.
- **Client-side/UI-enforced role-based visibility as the primary access
  control.** Rejected outright: explicitly forbidden — UI hiding is never
  considered an authorization control, and is trivially bypassed via direct
  API calls.
- **Simple Role-Based Access Control (RBAC) only, without Policy/Data Scope
  layering.** Rejected as insufficient: the platform's routing/access needs
  (Organization, Branch, Resource Ownership, Consent) are finer-grained
  than role alone can express, especially for multi-tenant, multi-branch,
  consent-sensitive medical data.
- **Unified Login + Backend-Enforced Policy-Based Access (Role + Permission
  + Policy + Data Scope + Organization + Branch + Resource Ownership +
  Consent).** **Chosen.** Matches the vision's routing model exactly and
  gives enough granularity for multi-tenant, multi-branch, consent-aware
  authorization.

## Positive Consequences

- One place (Backend Platform) to reason about "can this user do this
  action," instead of N client-specific implementations.
- Fine-grained Data Scope supports multi-tenant/multi-branch/consent
  requirements without ad hoc per-feature access logic.
- UI-hiding-as-security is structurally excluded from the design, reducing
  a common class of access-control bugs.

## Negative Consequences

- More upfront design/implementation work than simple role checks (Policy +
  Data Scope + Resource Ownership + Consent evaluation for every sensitive
  operation).
- A single Unified Login/Backend Platform becomes a critical dependency for
  every client surface.

## Risks

- **Client-supplied role/permission claims trusted without backend
  verification.** Mitigated by explicit prohibition (Constitution Section
  20) and security tests attempting exactly this forgery.
- **Break-glass misuse as a routine bypass.** Mitigated by mandatory
  time-limiting, justification capture, and audit review (Constitution
  Section 21).

## Verification

- Security tests calling backend endpoints directly (bypassing the UI) to
  confirm authorization still holds.
- Policy engine test suite asserting an unlisted action is denied by
  default (Deny by Default).
- Audit log review confirming every Break-Glass use has justification, time
  bound, and follow-up review.

## Revisit Triggers

- A specific client surface or user type proves to need an access model
  this Policy-Based structure cannot express — handled as a Policy-model
  extension, not a reversal of Unified Login or Backend-Enforced
  Authorization.
