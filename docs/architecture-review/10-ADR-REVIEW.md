# ADR Review

Every ADR touched (directly cited or implicitly relied upon) by the
reuse program, reviewed for continued validity against the Technology
Baseline. Recommendation options: Accepted (no change), Superseded,
Amended, Deprecated. **Board recommendation for all 12: no status
change** — full reasoning below, with ADR-0011 given the deepest
treatment per this phase's explicit Task 12.

| ADR | Title | Current Status | Board Recommendation | Reuse-Program Usage |
|---|---|---|---|---|
| 0001 | Modular Monolith First | Accepted | **No change** | Respected throughout — no reuse decision introduced a microservice split; every Engine is integrated as a bounded, adapter-isolated dependency, not a service-mesh participant. |
| 0002 | Domain-Driven Design | Accepted | **No change** | Respected — every REFERENCE+BUILD decision (Modules 9-15, 23) explicitly preserves Aggregate/Bounded-Context ownership rather than importing a foreign domain model wholesale. |
| 0003 | Schema per Module | Accepted | **No change** | Not directly exercised by the reuse program (a data-layer decision, not a Build-vs-Buy one) but not contradicted — no adopted Engine was found to require a shared-schema integration model that would conflict. |
| 0004 | Event-Driven Integration | Accepted | **No change** | Respected — RabbitMQ (Module 4) is explicitly logged as the platform-wide durable-delivery backbone consistent with this ADR's intent. |
| 0005 | Hybrid Tenant Isolation | Accepted | **No change** | Directly engaged — Module 2's PostgreSQL RLS finding is explicit evidence *for* this ADR's shared-tier model, not a contradiction. See `09-OPEN-QUESTIONS.md` #15 for the still-open implementation detail this ADR itself deferred. |
| 0006 | Independent Device Gateway | Accepted | **No change** | Directly engaged — Module 4's Mirth Connect/Apache Camel decision explicitly implements this ADR's Independent Component pattern; the frozen-release risk (`11-RISKS.md` R-02) is a vendor-selection risk, not a challenge to the ADR's architecture. |
| 0007 | Governed AI Gateway | Accepted | **No change** | Directly engaged — Module 6's Portkey Gateway decision explicitly implements this ADR; Constitution Section 28's HITL guardrails are referenced as the selection criterion, not weakened by it. |
| 0008 | Unified Login and Policy-Based Access | Accepted | **No change** | Directly engaged — Module 1's Keycloak + OPA decision is this ADR's direct implementation; OPA's 8-Module reuse count is the strongest evidence in the entire program that this ADR's policy-based-access model scales cleanly. |
| 0009 | SaaS-First, On-Premise-and-Hybrid-Ready | Accepted | **No change** | Directly relevant to `07-LICENSE-REVIEW.md`'s GPL-3.0 analysis (self-hosted/SaaS use is Clear; an on-premise *distribution* model would need re-review) — this Board flags that dependency explicitly rather than letting it sit implicit. |
| 0010 | Arabic/English and Localization-First | Accepted | **No change** | Not directly exercised by the reuse program (no Engine's localization capability was a selection criterion in the visible record) — no conflict found, but this Board notes it as a **gap to verify at SAD time**: confirm each ratified Engine (Keycloak, ERPNext, Frappe HR, etc.) actually supports Arabic RTL/localization before final commitment, since this was not a checked criterion during Build-vs-Buy research. |
| 0011 | Core Domain — Test Processing and Result Verification (Amended: "Patient-to-Result Orchestration") | **Proposed — Amended** | **No change — remains Proposed, NOT promoted to Accepted by this Board** | See dedicated section below. |
| 0012 | Candidate Bounded Context Map | **Proposed — Amended** | **No change** | Used as the Module/Feature organizing structure for the entire reuse program (`MASTER_FEATURE_CATALOG.md`'s 28 Modules trace to this map) — used as a working structure throughout, consistent with its own Proposed status, never treated as more settled than that. |

## ADR-0011 — Dedicated Review (Task 12: Core Domain Preservation)

**Current status, verified by direct read of the ADR file:** `Proposed
— Amended (Gap Closure Wave 14, 2026-07-16)`. Explicitly **not**
Accepted — the ADR's own text states this is intentional: *"Marking
this ADR Accepted would let an assumption-driven finding silently
graduate to governing-rule status, exactly the failure mode this
project's entire Constitution and Context Store discipline exists to
prevent."*

**Board finding: NO Core Domain leakage occurred across the reuse
program.** This Board checked every Feature classified REFERENCE+BUILD
on Core Domain grounds and confirms none of them substituted a
wholesale third-party system for the ADR-0011 Aggregate chain
(`TestResult`, `TestProcessingStarted → TestResultCaptured →
ResultVerified → ResultReleased`):

| Module | Wholesale Candidate Evaluated | Outcome |
|---|---|---|
| Patient Management (9) | OpenMRS | **Rejected** — explicitly would displace the Core Domain |
| Diagnostic Ordering (12) | OpenELIS Global, Bahmni | **Rejected** — Reference pattern only |
| Specimen Operations (13) | (deferred to 14) | N/A |
| Laboratory Execution (14) | SENAITE, OpenELIS Global | **Rejected** — the program's most deliberately-weighed decision, explicitly reasoned through both directions before rejecting wholesale adoption |
| Result Verification and Reporting (15) | (no new wholesale candidate found) | N/A — BUILD by default |
| Insurance and Corporate Contracts (23) | openIMIS | **Adopted wholesale — but correctly, since Insurance/Claims administration is explicitly outside the Patient-to-Result event chain**, not a Core Domain leakage |

**This Board's independent verification, not a re-statement of the
reuse program's own claim:** the openIMIS adoption (row 6 above) is the
one case requiring genuine scrutiny — a whole-system Engine *was*
adopted. This Board re-traces the boundary argument
(`insurance-and-corporate-contracts/eligibility-verification/
08-build-vs-buy.md`): insurance eligibility/claims administration is a
payer-side administrative function, not a step in the `TestResult`
Aggregate's own event chain. **This Board concurs the boundary holds.**
No Core Domain leakage confirmed.

**Standing governance note this Board adds (not present verbatim in the
reuse program's own output):** because ADR-0011 is Proposed, not
Accepted, its "Patient-to-Result Orchestration" framing is itself
subject to change pending the still-open Specimen Management alternative
(`09-OPEN-QUESTIONS.md` #14). **If the user later selects Specimen
Management (with Home Collection Logistics as the differentiator) as
the actual Core Domain instead**, the 7 Modules listed in the table
above would need to be **re-examined, not automatically re-approved** —
their REFERENCE+BUILD reasoning depends on which Bounded Context is
actually Core. This dependency is now explicit in the Technology
Baseline's governance record (`12-DECISION-FREEZE.md`), where it was
previously implicit across many individual Feature files.

## Board Summary

- **ADRs reviewed: 12**
- **Recommended for status change: 0**
- **ADR-0011's Proposed status is explicitly re-confirmed, not silently
  promoted** — this is the single most important finding of this
  review's ADR section.
- **One new dependency made explicit**: every Core-Domain-preservation
  decision in the Technology Baseline is conditional on ADR-0011's
  eventual Acceptance in its current or a materially similar form.
