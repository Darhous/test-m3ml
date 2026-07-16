# Bounded Contexts (Discovery, Phase 06)

**Status: Draft — Assumption-Driven Autonomous Run.** Formalizes the 8
evidenced Subdomains from Phase 04/05 into Bounded Contexts. Subdomains
9–11 (Inventory, QC/Accreditation, Staff/Operations) remain unformalized —
zero Event Storming evidence, per Phase 04/05's own caveats; forcing a
Bounded Context boundary around them now would be structure without
evidence.

## Resolved: the Specimen Management / Test Processing Boundary Question

**Decision (Discovery-level, Proposed — not Constitution-Accepted until
Phase 12 ADR):** they are **separate** Bounded Contexts. Rationale:
(1) different Core/Supporting classification (Phase 04) — concentrating
deep modeling investment in the Core context requires a real boundary, not
just a naming distinction; (2) different primary actors (Specimen:
collection/logistics roles; Test Processing: clinical/verification roles);
(3) the `SpecimenAccessioned` Pivotal Event marks a genuine responsibility
handoff; (4) Phase 05 already confirmed their Aggregates reference each
other only by ID, with no embedding — the tactical evidence already pointed
this way before the strategic decision made it explicit.

## The 8 Bounded Contexts

| Context | Classification | Owned Aggregates | Ubiquitous Language (core terms) |
|---|---|---|---|
| **Order Management** | Supporting | TestOrder, TestCatalogEntry | Order, Test Catalog, Ordering Actor |
| **Specimen Management** | Supporting | Specimen | Specimen, Collection, Accessioning, Rejection, Chain of Custody |
| **Test Processing and Result Verification** | **Core** | TestResult | Result, Verification, Release, Provenance |
| **Notification and Communication** | Generic | NotificationRequest | Notification, Recipient, Channel |
| **Billing and Claims** | Supporting | Invoice, Claim | Invoice, Claim, Adjudication, Settlement |
| **Device and Equipment Integration** | Supporting | DeviceImportRecord | Device, Adapter, Import, Provenance |
| **Core Platform — Identity and Access** | Generic | (governed at Constitution level: User, Role, Permission, Policy) | Identity, Role, Permission, Policy, Data Scope |
| **Core Platform — Organization and Branch** | Generic | (governed at Constitution level: Organization, Branch) | Organization, Branch, Tenant |

**Note on the two "Core Platform" rows:** per Constitution Section 10,
Core Platform is a single logical grouping ("Identity, Audit, Policy,
Notification-core") that any module may depend on. Discovery treats
Identity/Access and Organization/Branch as two Bounded Contexts *within*
Core Platform (they have distinct Ubiquitous Language and distinct owned
concepts) rather than inventing a third top-level classification — this is
additive detail under an already-Accepted rule, not a new decision.

## Context Map — Every Relationship, Named

| From (consumer) | To (provider) | Pattern | Rationale |
|---|---|---|---|
| Order Management | Core Platform — Identity and Access | Open Host Service + Published Language | Identity exposes a stable, versioned contract consumed uniformly by every context (Constitution Section 10/20). |
| Order Management | Core Platform — Organization and Branch | Open Host Service + Published Language | Same reasoning — Organization/Branch reference data needed for Data Scope (Constitution Section 18). |
| Specimen Management | Order Management | Customer/Supplier | Specimen exists to satisfy an already-placed Order; Order Management does not need to know about Specimen's internal state. |
| Specimen Management | Core Platform (both) | Open Host Service + Published Language | Same as above. |
| Test Processing and Result Verification | Specimen Management | Customer/Supplier | Result depends on an Accessioned Specimen existing; Specimen Management is upstream. |
| Test Processing and Result Verification | Order Management | Customer/Supplier | Result also references the originating Order. |
| Test Processing and Result Verification | Core Platform (both) | Open Host Service + Published Language | Same as above. |
| Test Processing and Result Verification | Device and Equipment Integration | **Anti-Corruption Layer** (consumer side) / Open Host Service (provider side) | Mandatory per Constitution Section 6/24 — device data must never leak its native model into the Core Subdomain untranslated. Event-based (Integration Event), not a compile-time dependency (Device Integration is an Independent Component, Constitution Section 11). |
| Notification and Communication | Specimen Management, Test Processing and Result Verification, Billing and Claims | Open Host Service + Published Language (event-based) | Notification subscribes to Integration Events from all three; it is an Independent Component (Constitution Section 11), no compile-time dependency edge. |
| Billing and Claims | Test Processing and Result Verification | Open Host Service + Published Language (event-based) | `BillableEventIdentified` triggered by `ResultReleased` — event-based, not a direct Aggregate reference. |
| Billing and Claims | Order Management | Customer/Supplier | Invoice line items reference TestOrder/TestCatalogEntry. |
| Billing and Claims | Core Platform (both) | Open Host Service + Published Language | Same as above. |

**Shared Kernel — explicitly considered and rejected:** Organization/
Branch reference data is used by every context, which could tempt a Shared
Kernel design. Rejected in favor of Open Host Service + Published Language,
consistent with Constitution Section 7's caution to keep Shared Kernel
"small and explicitly governed" and to prefer it only when genuinely
justified — a read-mostly, stable reference contract does not need the
tighter coupling a Shared Kernel implies. No ADR is triggered by this
non-choice (an ADR is only required if a Shared Kernel *is* adopted,
Constitution Section 7).

## Module Ownership Draft (Constitution Section 8)

| Candidate Module | Owns Bounded Context(s) | Independent Component? |
|---|---|---|
| Order Management Module | Order Management | No |
| Specimen Management Module | Specimen Management | No |
| Laboratory Testing Module | Test Processing and Result Verification | No |
| Billing and Claims Module | Billing and Claims | No |
| Notification Service | Notification and Communication | **Yes** — already an Accepted Independent Component (Constitution Section 11) |
| Device Integration Gateway | Device and Equipment Integration | **Yes** — already an Accepted Independent Component (ADR 0006) |
| Core Platform | Identity and Access, Organization and Branch | No (Core Platform is not "independent," it's the universal dependency, Constitution Section 10) |

## Acyclic Dependency Graph Confirmation

Compile-time dependency edges only (event-based Independent Component
relationships excluded, per Constitution Section 11):

```
Core Platform  ← Order Management
Core Platform  ← Specimen Management
Core Platform  ← Test Processing and Result Verification
Core Platform  ← Billing and Claims
Order Management  ← Specimen Management
Order Management  ← Test Processing and Result Verification
Order Management  ← Billing and Claims
Specimen Management  ← Test Processing and Result Verification
```

**Confirmed acyclic** — Core Platform has zero outgoing edges (matches
Constitution Section 9/10 exactly); no cycle exists in the remaining graph
(traced manually: Order Management → Core Platform only; Specimen
Management → {Order Management, Core Platform}; Test Processing →
{Specimen Management, Order Management, Core Platform}; Billing and Claims
→ {Order Management, Core Platform} — every arrow points toward Core
Platform, no arrow points back out).

## Divergence from `module-catalog.md` (confirmed, extends Phase 04's note)

- "Laboratory Modules" (1 category) → 3 Modules (Order Management,
  Specimen Management, Laboratory Testing).
- "Insurance Modules" → folded into Billing and Claims Module (pending
  `open-questions.md` #17).
- "Workflow Modules" → not a standalone Module; workflow/state-transition
  behavior lives inside Specimen Management and Laboratory Testing
  (confirmed at Phase 06, not just suspected as in Phase 04).
- "Core Platform Modules" + "Identity and Access Modules" + "Organization
  Modules" → confirmed as a single Core Platform grouping with two internal
  Bounded Contexts, matching Constitution Section 10 exactly.
- "Patient Modules" and "Doctor and Clinic Modules" → **still no distinct
  Bounded Context** — Patient and Doctor remain Actors referenced across
  multiple contexts (Order Management, Specimen Management, Notification),
  not concepts with their own owned Aggregate. This is logged as a
  confirmed gap, not forced into an artificial context.
