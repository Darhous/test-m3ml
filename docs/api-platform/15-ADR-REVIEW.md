# ADR Review — API-First Architecture Compatibility

Every ADR is reviewed here for compatibility with the API-First
architecture defined in this document set. This is a **compatibility
check**, not a re-litigation of any ADR's underlying Decision — this
Board does not have, and does not exercise, authority to change any
ADR's Decision section (per this phase's Do-Not list). Recommendation
options: Accepted (no change), Superseded, Amended, Deprecated.
**Recommendation for 11 of 12 ADRs: no change.** ADR-0011 receives the
dedicated treatment this phase's Task explicitly requires, below.

| ADR | Title | Current Status | API-First Compatibility | Recommendation |
|---|---|---|---|---|
| 0001 | Modular Monolith First | Accepted | Fully compatible — `02-API-FIRST-ARCHITECTURE.md`'s five-layer model is built directly on Modular Monolith's Module-boundary premise; API-First does not require, and this phase does not introduce, a service-mesh or microservice split. | No change |
| 0002 | Domain-Driven Design | Accepted | Fully compatible — every API resource in `03-API-DOMAIN-INVENTORY.md` and every naming rule in `06-NAMING-CONVENTIONS.md` is Aggregate- and Ubiquitous-Language-derived, not database-derived. | No change |
| 0003 | Schema per Module | Accepted | Fully compatible, and directly enforced by `02-API-FIRST-ARCHITECTURE.md`'s Boundary Rules ("no direct cross-module database access") and by `06`'s namespace-mirrors-Module rule. | No change |
| 0004 | Event-Driven Integration | Accepted | Fully compatible — `06-NAMING-CONVENTIONS.md` reuses existing Domain Event names verbatim rather than inventing API-specific event names; RabbitMQ remains the integration backbone this phase does not redesign. Event Catalog/Webhook design is explicitly Part 2. | No change |
| 0005 | Hybrid Tenant Isolation | Accepted | Fully compatible — `14-MULTI-TENANCY.md` is a direct API-layer application of this ADR, deliberately designed to be agnostic to Open Question #15's still-open partitioning-technology detail. | No change |
| 0006 | Independent Device Gateway | Accepted | Fully compatible — `02`'s Anti-Corruption Layer (Layer 5) and `08-AUTHENTICATION.md`'s Machine Identity treatment both implement this ADR's isolation pattern directly. | No change |
| 0007 | Governed AI Gateway | Accepted | Fully compatible — `03`'s AI Operations Gateway classification and `11-API-SECURITY.md`'s API6 (Sensitive Business Flows) control both preserve this ADR's Human-in-the-Loop requirement at the API layer. | No change |
| 0008 | Unified Login and Policy-Based Access | Accepted | Fully compatible — `08-AUTHENTICATION.md` and `09-AUTHORIZATION.md` are direct, non-contradictory elaborations of this ADR at the API layer; no alternative identity or authorization model is introduced. | No change |
| 0009 | SaaS First, On-Premise Ready, and Hybrid Ready | Accepted | Fully compatible — no API standard in this document set assumes a specific cloud provider or deployment topology; the Gateway-product and Secrets-Engine gaps (`10`, `12`) are Technology Baseline gaps, not deployment-topology conflicts. | No change |
| 0010 | Arabic/English and Localization First | Accepted | Fully compatible — `05-API-STANDARDS.md`'s Localization and Time Zone standards implement this ADR directly at the API layer, closing the "not directly exercised" gap the EARB's own `10-ADR-REVIEW.md` flagged for the reuse program. | No change |
| 0012 | Candidate Bounded Context Map | **Proposed — Amended** | No architectural conflict found — `03-API-DOMAIN-INVENTORY.md` uses the same 28-Module structure this map organizes, consistent with its own Proposed status (used as working structure, never treated as more settled than that, mirroring the EARB Board's own treatment). | No change — remains Proposed, for the same reason as ADR-0011 below |

## ADR-0011 — Dedicated Review

**Current status, verified by direct read of the ADR file:** `Proposed
— Amended (Gap Closure Wave 14, 2026-07-16)`. This Board's task is
explicit: *if* ADR-0011 is now fully supported by all previous phases
and no architectural conflict remains, recommend Accepted with
complete justification — but do not force the change if the bar is not
met.

### Step 1 — Is there an architectural conflict between ADR-0011 and API-First architecture specifically?

**Finding: No.** This Board checked every place API-First architecture
touches the Core Domain cluster:

- `03-API-DOMAIN-INVENTORY.md`'s classification of the 7 Core Domain
  Modules (Patient Management through Result Verification and
  Reporting) works identically regardless of whether "Patient-to-
  Result Orchestration" or the competing "Specimen Management"
  framing is ultimately ratified as Core — the API contracts are
  Aggregate-shaped (`TestOrder`, `Specimen`, `TestResult`), and Wave 5's
  candidate Aggregates already name `Specimen` as its own Aggregate
  Root regardless of which Bounded Context is labeled Core.
- `02-API-FIRST-ARCHITECTURE.md`'s Anti-Corruption Layer pattern
  applies uniformly to every REFERENCE+BUILD decision in the Core
  Domain cluster — it does not depend on which Module is "the" Core
  Domain.
- `11-API-SECURITY.md`'s Human-in-the-Loop control (API6) protects
  `ResultVerified`/`ResultReleased` regardless of the ADR's Proposed
  vs. Accepted status — the control is already in force by virtue of
  ADR-0007, independent of ADR-0011.

**Conclusion of Step 1: architecturally, API-First design is fully
compatible with ADR-0011 as currently framed, and would remain
compatible even if the Specimen Management alternative were chosen
instead.** This is itself informative: the API layer's design does not
turn out to depend on resolving which Bounded Context is Core, which
means this phase's own evidence cannot supply the missing resolution
either — see Step 2.

### Step 2 — Is ADR-0011 "fully supported by all previous phases"?

This is a higher bar than "no architectural conflict," and the ADR's
own text is explicit about what would meet it: promotion to Accepted
requires the user to review the ADR-0011 finding and "ideally resolve
the Specimen Management alternative," through "the normal Constitution
Section 45 Amendment/Section 39 ADR process — not by silently editing
this file's Decision section."

**This Board's finding: that bar is not met by this phase's own
inputs.**

- `.claude/context/open-questions.md` Question #14 remains explicitly
  **Open** as of this review — not answered, not silently closed.
- The competing Specimen Management alternative
  (`.claude/context/module-catalog.md`'s Discovery Candidate Context
  #2, `.claude/context/glossary.md`'s Discovery Phase 04 Candidate
  Subdomains) has not been resolved by this phase, the EARB phase
  before it, or any phase between Discovery Wave 7 and now. No new
  business-strategy evidence has entered the record.
- This is a **business-strategy question** — which Bounded Context
  carries the platform's actual competitive differentiation — not an
  architecture question. Neither the EARB Board nor this Board holds
  the authority or the evidence to answer it; both Boards can only
  confirm that the architecture built *on top of* whichever answer
  emerges remains sound, which Step 1 above does.

### Recommendation

**No status change. ADR-0011 remains Proposed — Amended.**

This is not a default or a copy of the EARB phase's prior finding
restated without independent reasoning — this Board independently
verified the specific, narrower question this phase's Task assigned
("if ADR-0011 is now fully supported by all previous phases and no
architectural conflict remains") and found: the architectural-conflict
half of the bar is cleared, but the "fully supported by all previous
phases" half is not, because the one thing every previous phase
(Discovery Wave 7, the EARB Board, and now this Board) has consistently
found still open — the Specimen Management alternative — remains open.
Per the user's own explicit instruction not to force this change, and
consistent with `docs/architecture-review/10-ADR-REVIEW.md`'s
established reasoning (which this Board independently re-derived
rather than merely cited), **this Board does not recommend promoting
ADR-0011 to Accepted.**

## Board Summary

- **ADRs reviewed: 12.**
- **Recommended for status change: 0.**
- **ADR-0011 given dedicated treatment per this phase's explicit Task:
  architecturally compatible with API-First design, but not promoted
  to Accepted** — the blocking gap is business-strategy evidence, not
  architecture, and remains genuinely unresolved.
- **New governance note this Board adds:** because API-First
  architecture is now independently confirmed compatible with *either*
  candidate Core Domain framing (Patient-to-Result Orchestration or
  Specimen Management), a future resolution of Open Question #14 in
  either direction will **not** require rework of this document set —
  `03-API-DOMAIN-INVENTORY.md`'s classifications and `02`'s layering
  hold either way. This is a genuinely new finding this phase
  contributes, not a restatement of the EARB Board's prior work.
