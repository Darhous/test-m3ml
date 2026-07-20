# SAD Wave 3 — Solution Strategy

## 1. Document Metadata

| Field | Value |
|---|---|
| Wave number and title | 3 of 13 — Solution Strategy (`docs/sad/README.md`) |
| Document Status | **Review** (Constitution §59 Document Status Vocabulary — not `Accepted`) |
| Owner | Author of this Wave (session author, 2026-07-20) |
| Review authority | Project Owner, acting as Architecture Review Board (Constitution §57 — the ARB is a function/process fulfilled entirely by the project owner today) |
| Dependencies | Wave 1 (`01-introduction-goals-constraints-stakeholders.md`) — **Accepted**, 2026-07-20; Wave 2 (`02-context-and-scope.md`) — **Accepted**, 2026-07-20 (commit `5434739`) |
| Supersedes | None |
| Superseded by | None |
| Updated | 2026-07-20 |

This Wave does not become `Accepted` in this pass, regardless of its own self-review verdict (§25). Per the Inter-Wave Gate (`docs/sad/README.md`), only the Project Owner's explicit statement of acceptance changes this field.

## 2. Purpose and Boundaries

**Function of this Wave.** Solution Strategy answers *how* the platform's already-Accepted architectural decisions (14 ADRs, Constitution v2.1, the frozen Technology Baseline, the API Platform Strategy) compose into one coherent strategic direction. It is a **synthesis and interpretation pass**, not a design pass: every Strategy Pillar in §6–§18 traces to a decision, requirement, or frozen baseline input that already exists; none is authored here for the first time.

**Difference from Wave 2 (Context & Scope).** Wave 2 answered *what* the System of Interest is: its boundary, actors, external systems, and scope classification. This Wave answers *how* that system is strategically realized — architectural style, domain strategy, communication strategy, data strategy, and so on — without re-drawing the boundary or re-classifying scope. Where this Wave repeats a Wave 2 fact (e.g., the 28 Bounded Contexts, the 24 Engines), it cites Wave 2 or the same upstream source Wave 2 cited, not a new independent judgment.

**Difference from Wave 4 (Building Block View).** Wave 4 will decompose the System of Interest into concrete Containers, Components, and a Module/Bounded-Context-to-implementation mapping. This Wave explicitly does **not** perform that decomposition: no C4 Container or Component diagram appears here, no deployable-unit count is fixed, and the question of whether a given Bounded Context maps 1:1 to an implementation Module is left exactly as undecided as Wave 2 §8 left it.

**Topics deferred to Waves 4–13.** Full list in §24 (Wave Boundary Map). In summary: internal decomposition (Wave 4), runtime sequences (Wave 5), deployment topology (Wave 6), security/privacy/trust-boundary detail (Wave 7), IAM/multi-tenancy implementation detail (Wave 8), AI/device/cross-cutting implementation detail (Wave 9), consolidated traceability (Wave 10), quality scenarios (Wave 11), risk treatment (Wave 12), and final consistency/glossary close-out (Wave 13).

**This document creates no new architectural decision.** Every Strategy Pillar's "Accepted Strategy" statement cites the ADR, Constitution section, Decision ID, or frozen baseline entry that already established it. Where no such source exists for a plausible strategic statement, that statement is not made — it is recorded instead in §21 (Explicit Non-Decisions) or §22 (Open Dependencies).

## 3. Executive Solution Strategy

The platform's Solution Strategy, stated in one page, each point traced to its Accepted source (full citation in §23's Traceability Matrix):

1. **Domain-aligned Modular Monolith First** — one deployable unit organized around Bounded Contexts, not a microservices default. *[ADR-0001]*
2. **Selective independent components** — 8 named Independent Components/Shared Services may be operationally independent from v1 for documented reasons (protocol isolation, external-facing surface, variable load, governed external calls). Any other Module remains inside the single Modular Monolith deployable unless and until **Selective Service Extraction** — pulling it out into its own independently-deployed service — is justified by a measured, documented operational or organizational trigger and recorded in a new ADR (§18); no such extraction is planned or Accepted today. *[Constitution §5, §11; ADR-0001]*
3. **Clean/Hexagonal dependency direction** — Domain and Application logic depend on nothing outward; Frameworks, Engines, and databases sit at the outer boundary, reached only through Ports and Adapters. *[Constitution §5 "No Direct Cross-Module Database Access"; `architecture-patterns` skill, applied in §8]*
4. **Event-driven cross-boundary integration** — Domain Events stay inside a Bounded Context; Integration Events cross boundaries only through deliberate, versioned translation; synchronous calls remain available for immediate-answer needs. *[ADR-0004; Constitution §12–13]*
5. **API-governed client/external access** — one unified backend, no Portal-specific fork; every external Engine sits behind the platform's own API and an Anti-Corruption Layer; Kong Gateway is the approved Edge Gateway. *[`01-API-VISION.md`; `02-API-FIRST-ARCHITECTURE.md`; D-44]*
6. **PostgreSQL-centered data foundation** — the primary transactional relational engine for Module-owned schemas platform-wide, with Row-Level Security as the shared-tier tenancy mechanism. *[ADR-0013; ADR-0003; D-42]*
7. **Hybrid tenant isolation** — shared infrastructure with strict logical isolation for small/medium tenants; dedicated database/deployment available for large/regulated tenants. *[ADR-0005]*
8. **Unified identity and policy-based authorization** — one login entry point; every state-changing and sensitive-read operation authorized server-side via Role, Permission, Policy, Data Scope, Organization, Branch, Resource Ownership, and Consent; UI hiding is never a control. *[ADR-0008; Constitution §21]*
9. **SaaS-first, On-Premise/Hybrid-ready** — the same logical architecture deploys across three modes; the cloud provider remains replaceable where practical. *[ADR-0009]*
10. **Open-source reuse behind adapters and ACLs, with the Core Domain protected from displacement** — 24 Engines, each individually Approved / Conditionally Approved / License-Dependent (never a uniform "ratified" status; full breakdown in §13), each wrapped by the platform's own contract; of the six Core-Domain-adjacent Modules given a dedicated wholesale-adoption review, five (Patient Management, Diagnostic Ordering, Specimen Operations, Laboratory Execution, Result Verification and Reporting) rejected wholesale Engine adoption to protect ADR-0011's Aggregate chain, and the sixth (Insurance and Corporate Contracts) correctly adopted openIMIS wholesale precisely because it sits outside that chain. *[`02-TECHNOLOGY-BASELINE.md`; `docs/architecture-review/10-ADR-REVIEW.md`]*
11. **Governed AI and isolated device integration** — both are independent, governed gateways with mandatory Human-in-the-Loop (AI) and a mandatory Anti-Corruption Layer plus provenance (devices); neither is embedded ungoverned inside a business Module. *[ADR-0006; ADR-0007]*
12. **Evolution by evidence-based selective extraction** — a Module is extracted from the Monolith, CQRS is adopted, or a dedicated Search/Cache/Analytics component is added only on a measured, documented trigger — never in anticipation. *[Constitution §55, Evolution Strategy]*

## 4. Domain Vision Statement

Produced within this Wave per `docs/certification/15-SAD-INPUT-PACKAGE.md` item 10 ("a dedicated one-page Domain Vision Statement — still a minor Dependency, unresolved" as of Wave 2), using the `domain-driven-design` skill's Strategic Design framework (§25, Skills Utilization Report). This is **part of Wave 3**, not an independent Product Strategy document — it closes an inherited Dependency, it does not open a new one.

> **The platform's differentiating value is orchestrating a patient's journey from an ordered diagnostic test to a verified, released, and trusted result** — coordinating the Patient and Doctor/Practitioner participants explicitly as first-class actors in that chain, not merely as records attached to a laboratory workflow. The competitive question this domain model must answer is not "can we run a lab efficiently" (every competitor can) but "can we make the whole test-to-trusted-result journey — ordering, collection, processing, verification, and delivery — coherent, auditable, and configurable across many kinds of healthcare organizations, at SaaS scale, in two languages, without lowering the bar for clinical trust." Everything the platform builds around this chain (Billing, Insurance, Inventory, Workforce, and the 19 Recognized-tier Bounded Contexts) exists to support that journey being reliable and operable, not to compete with it for architectural investment.

Constraints this statement observes, all carried forward, none newly asserted:

- **Traces to ADR-0011** ("Patient-to-Result Orchestration," Accepted 2026-07-18) and its own event chain (`TestProcessingStarted → TestResultCaptured → ResultVerified → ResultReleased`, the `TestResult` Aggregate).
- **Preserves ADR-0011's evidentiary caveat in full**: the underlying evidence remains `Inferred — Industry Reference`; this statement does **not** assert the Specimen Management/Home Collection Logistics alternative is resolved or scored lower — that hypothesis remains live and unresolved, exactly as ADR-0011's own text states (Wave 1 §4.2, Wave 2 §4, both cited, not re-litigated here).
- **Does not claim a general-purpose product for every hospital need.** The vision statement is scoped to the orchestration chain and the Modules that support it — not a claim that the platform serves every Hospital Information System function.
- **Does not convert the HIS/full-ERP/general e-commerce Non-Goals into Future Roadmap.** They remain Explicit Non-Goals (Wave 2 §9, §10; `W1-vision-scope-operating-model.md`), unaffected by this statement.

## 5. Architectural Drivers

| Driver | Description | Status | Source |
|---|---|---|---|
| Multi-tenant SaaS at variable trust levels | Small/medium tenants need low-friction shared infrastructure; large/regulated tenants need stronger isolation | Accepted | ADR-0005 |
| Healthcare-domain trust and auditability | Medical data is highly sensitive; every sensitive action needs an immutable Audit Event | Accepted | Constitution §21–23; constraint #5 (Wave 1 §7) |
| Integration complexity (devices, AI, payers, partners) | Multiple heterogeneous external systems, each with different protocols and trust levels | Accepted (pattern), Open (specific protocols/partners) | ADR-0006; ADR-0007; Wave 2 §7 |
| Device and AI isolation from Core business logic | Neither device data nor AI output may corrupt or auto-finalize a clinical/business record | Accepted | ADR-0006; ADR-0007; Constitution §24, §28 |
| Maintainability and evolvability under uncertainty | Domain, team structure, and load are not yet fully known; boundaries must not be paid for prematurely | Accepted | ADR-0001; Constitution §55 |
| Deployment portability | Tenants range from SaaS-comfortable to regulated on-premise/hybrid | Accepted | ADR-0009 |
| Legal/licensing dependencies | 5 adopted Engines carry unreviewed AGPL-3.0 exposure (R-04); 2 more carry unconfirmed licenses (R-07) — 7 distinct Engines total. **Not the same population** as the "7 Tier-1 Engines" named in §13/§18/§22 for R-08's exit-strategy dependency (Keycloak, OPA, ERPNext, OpenBoxes, Kill Bill, Frappe HR, openIMIS — a criticality classification, not a license-status one); the two sets share only one member (openIMIS) and otherwise differ, and coincide in count (7) only by chance | Open (Legal Dependency) | R-04, R-07 |
| Business/stakeholder concern coverage | 39 personas across 10 clusters, each with distinct concerns | Confirmed (roles) / Inferred (concerns) | Wave 1 §5–§6; Wave 2 §6 |

**No quality-attribute numeric target (latency, throughput, availability, RTO/RPO) is asserted in this section or anywhere in this Wave.** Constitution §51 keeps these explicitly `Draft` pending real usage data (Open Question #4); ADR-0014 gives Disaster Recovery a tier *framework* with numeric cells honestly labeled Pending. Wave 11 (Quality Requirements & Quality Scenarios) is the owning Wave for turning these drivers into scenarios; this Wave only names the drivers themselves.

## 6. Overall Architecture Style

### Driver / Problem
The platform must support a healthcare SaaS domain of eventually-broad scope (32 confirmed business domains, Wave 2 §9) without either (a) paying full distributed-systems cost before the domain and team structure justify it, or (b) collapsing into an unstructured monolith that cannot later be decomposed.

### Accepted Strategy
**Modular Monolith First**, with 8 named Independent Components/Shared Services operationally separate from v1 for documented reasons, and Selective Service Extraction available for any other Module once a measured trigger exists.

### Rationale
ADR-0001's own Alternatives Considered rejected both extremes: microservices-from-day-one (distributed-systems cost paid before it is earned) and an unstructured monolith (produces a Big Ball of Mud, blocking later extraction entirely). The 8 Independent Components are not a general microservices posture — each is justified individually by a concrete operational need (Constitution §11): Notification Service (fan-out, multi-channel), Device Integration Gateway (protocol isolation, ADR-0006), AI Gateway (governed external calls, ADR-0007), Analytics Platform (variable/read-heavy load), Search Service (specialized query capability), File Processing Service (variable, potentially long-running load), Public API Gateway (externally-facing edge surface, realized as Kong Gateway, D-44), Background Workers (deferred/long-running work).

### How It Works at Strategy Level
One deployable unit (the Modular Monolith) hosts the majority of the 28 Bounded Contexts (Wave 2 §8), each with an enforced schema boundary (ADR-0003) and contract-only cross-Module access (ADR-0004). The 8 Independent Components run as separate deployables from v1, integrating with the Monolith and each other only through published APIs/Events — never a direct code dependency (Constitution §9, "Independent Components May Depend on Core Contracts Only"). Logical architecture (Bounded Context boundaries, contracts) is kept distinct from deployment topology (which is Wave 6's job) — "Modular Monolith" describes a dependency and contract discipline, not a literal single-process constraint that Wave 6 must honor unmodified.

### Consequences and Trade-offs
Positive: lower operational complexity while domain/team structure are still being discovered; extraction later is a deployment change, not a redesign, because boundaries are already enforced. Negative: requires ongoing architecture-test discipline to prevent boundary erosion (ADR-0001's own Risks section); some operational independence is unavailable for Modules not yet extracted.

### Guardrails
No module may be extracted "because microservices are best practice" or in anticipation of unmeasured scale (Constitution §55). Extraction requires a documented, measurable operational or organizational trigger and a new ADR (ADR-0001's own Revisit Triggers). The 8 named Independent Components are the only ones Accepted today; a 9th requires ADR-level approval (Constitution §57's Decision Types table).

### Deferred Detail / Owning Wave
Which Bounded Contexts become which concrete deployable Modules (if any beyond the 8 named components), container boundaries, and process topology: Wave 4 (Building Block View) and Wave 6 (Deployment View).

### Traceability
ADR-0001; Constitution §5 (Modular Monolith First, Selective Service Extraction), §9 (Module Dependency Rules), §11 (Shared Services Rules); Wave 2 §3, §5, §8.

### Status Classification
**Accepted Decision Synthesis.**

## 7. Domain-Driven Strategy

**Terminology, stated once here and used consistently throughout this Wave:** a **Bounded Context** is a Domain-Driven-Design modeling/language boundary — one of the 28 named contexts below — and is not itself a deployment concept (Constitution §6). A **Module** is the Modular Monolith's internal implementation unit (enforced schema boundary, ADR-0003; contract-only cross-Module access, ADR-0004); whether a given Bounded Context maps 1:1 to a Module is explicitly undecided (§21). An **Independent Component** is one of the 8 Constitution §11-named components that is operationally independent — a separate deployable — from v1 for a documented reason (§6). A **Service** in this Wave means any independently-deployed unit — either one of the 8 Independent Components, or a Module later pulled out via Selective Service Extraction (§6, §18) once a measured trigger fires; it is never used here as a synonym for "Bounded Context" or "Module."

### Driver / Problem
A platform spanning meaningfully different domains (Laboratory, Identity, Billing, Device Integration, etc.) needs a modeling approach that keeps each domain's language and rules distinct while still composing into one coherent system, and needs to know where to invest its deepest modeling effort.

### Accepted Strategy
**Domain-Driven Design** as the modeling approach (ADR-0002), with an **Accepted Core Domain** — Patient-to-Result Orchestration (ADR-0011; Accepted refers to the *decision*, not the underlying evidence, which remains `Inferred`; caveat preserved in full, §4 above) — and a two-tier **Bounded Context Map** of 28 contexts: 9 Modeled (Evidenced confidence, full tactical modeling already performed) and 19 Recognized (Inferred, named and boundary-sketched, tactical modeling still owed) (ADR-0012).

### Rationale
ADR-0002's Alternatives Considered rejected both generic technical layering (produces anemic models, no principled boundary basis) and data-model-first design (couples the domain to storage, conflicting with Schema per Module, ADR-0003). Strategic Design (per the `domain-driven-design` skill, §25) directs the deepest investment toward the Core Domain and lighter treatment toward Supporting/Generic subdomains — consistent with ADR-0012's own Modeled/Recognized tiering, which is not a deficiency but a deliberate application of that same principle: the 9 Modeled contexts received full tactical modeling because Discovery evidence concentrated there; the 19 Recognized contexts did not, and are not assumed complete by ADR-0012's acceptance.

### How It Works at Strategy Level
Every Bounded Context owns its own Ubiquitous Language and, per Constitution §6, distinguishes at minimum Entities, Value Objects, Aggregates (single root, small cluster), Domain Events, and Repositories. Cross-Bounded-Context relationships are labeled with an explicit context-mapping pattern (Constitution §7) — the reuse research consistently used **Anti-Corruption Layer** ("Adapter Boundary") language when integrating an external Engine into a Bounded Context's own model (e.g., Keycloak wrapped behind Identity and Access's own Anti-Corruption Layer, per `docs/reuse/MASTER_ENGINE_CATALOG.md`), never a **Conformist** relationship that would let a vendor's model leak into the domain layer. Where a whole-system Engine was evaluated for wholesale adoption inside a Core-Domain-adjacent Module — OpenMRS, Bahmni, OpenELIS Global, SENAITE — each was independently rejected specifically because wholesale adoption would have displaced the `TestResult` Aggregate chain (`docs/architecture-review/10-ADR-REVIEW.md`, "ADR-0011 — Dedicated Review"); openIMIS's whole-system adoption for Insurance and Corporate Contracts was judged **not** a Core Domain intrusion, because payer/claims administration sits outside the Patient-to-Result event chain, and this Wave does not re-open that judgment.

### Consequences and Trade-offs
Positive: module boundaries have a principled basis; the Core Domain receives concentrated modeling investment where it matters competitively; Supporting/Generic capability is reused rather than over-modeled. Negative: 19 Bounded Contexts still owe their full tactical modeling (Wave 4); the Specimen Operations/Laboratory Execution split remains, by ADR-0012's own words, "the single most consequential judgment call in the whole Context Map," carried forward unresolved.

### Guardrails
No Aggregate, Entity, Repository, or package layout is designed in this Wave. No Bounded Context-to-implementation-Module mapping is finalized here (Wave 2 §8's own caveat, restated, not resolved). The Specimen Management/Test Processing competing hypothesis is not decided by this Wave and is not this Wave's authority to decide (ADR-0011's own Revisit Trigger process, Constitution §39/§45).

### Deferred Detail / Owning Wave
Aggregate/Entity/Value-Object detail for all 28 contexts, Bounded-Context-to-Module mapping, package/schema layout: Wave 4 (Building Block View).

### Traceability
ADR-0002, ADR-0011, ADR-0012; Constitution §6–§7; Wave 2 §8; `docs/architecture-review/10-ADR-REVIEW.md`; `domain-driven-design` skill (Strategic Design, Bounded Contexts references, §25).

### Status Classification
**Accepted Decision Synthesis**, with ADR-0011/ADR-0012's evidentiary caveats preserved as **Inferred Rationale** within an otherwise Accepted decision (per Wave 1 §4.2's established pattern).

## 8. Clean and Hexagonal Architecture Strategy

### Driver / Problem
Business/domain logic must remain testable and swappable independently of any specific Engine, framework, or vendor — especially given that 24 Technology Baseline Engines, several with unresolved license status, sit behind the platform's own contracts and may need to be replaced.

### Accepted Strategy
Dependencies point inward: Domain and Application (use-case) logic depend on nothing from Adapters or Infrastructure; Frameworks, Engines, and databases are reached only through Ports (interfaces) and Adapters (implementations), consistent with the Dependency Rule the `architecture-patterns` skill formalizes (§25).

### Rationale
This is the direct architectural realization of two already-Accepted constraints: "No Direct Cross-Module Database Access" (Constitution §5, elevated as the single most load-bearing Modular-Monolith-integrity rule) and the Anti-Corruption Layer requirement at every external boundary (Constitution §6, explicitly naming Device Integration and AI Gateway). It is also the only way the platform can honor ADR-0009's "cloud provider replaceable where practical" and the Technology Baseline's individually-tracked "Replacement Candidate" column (e.g., Apache Camel documented against Mirth Connect's frozen-release risk, R-02) without a full redesign each time a vendor decision changes.

### How It Works at Strategy Level
Each Module's business/domain logic defines its own Ports (e.g., "a repository for this Aggregate," "a gateway for sending a notification"); concrete Adapters implement those Ports against a specific Engine (PostgreSQL via ADR-0013, Novu via the Notification Service, Keycloak/OPA via the Unified Login pattern). No Engine's native SDK, ORM model, or API type is imported into a Domain or Application layer. Testability follows as a property of this discipline, not a separate test plan: a Module's use cases can be exercised with an in-memory or stub Adapter, without a running Engine — stated here as a principle this strategy establishes, not a concrete test suite this Wave designs.

### Consequences and Trade-offs
Positive: any Engine behind a Port is replaceable without touching Domain logic — directly supporting the Technology Baseline's own Replacement Candidate tracking and the Exit Strategy deliverable still owed for the 7 Tier-1 Engines (R-08). Negative: every external integration requires an explicit Port/Adapter pair rather than a direct call — more upfront structure than calling an Engine's SDK inline.

### Guardrails
No folder layout, language-specific interface syntax, or dependency-injection mechanism is fixed here — that is Wave 4's job, guided by this principle. No Engine's native API may be exposed directly to a Portal, Partner, or Public consumer (`01-API-VISION.md`, `02-API-FIRST-ARCHITECTURE.md`, restated in §10).

### Deferred Detail / Owning Wave
Concrete Port/Adapter interfaces, dependency-injection wiring, folder structure: Wave 4 (Building Block View).

### Traceability
Constitution §5 (No Direct Cross-Module DB Access), §6 (Anti-Corruption Layer); ADR-0003, ADR-0006, ADR-0007, ADR-0009; `02-TECHNOLOGY-BASELINE.md` (Replacement Candidate column); `architecture-patterns` skill (§25).

### Status Classification
**Accepted Decision Synthesis.**

## 9. Communication and Integration Strategy

### Driver / Problem
Modules must react to each other's state changes without violating Schema per Module (ADR-0003) or creating tight coupling that undermines independent evolution — while some interactions genuinely need an immediate synchronous answer.

### Accepted Strategy
**Event-Driven Integration** (ADR-0004) as the default for cross-Module side effects, expressed as Domain Events (internal to a Bounded Context) translated deliberately into Integration Events (cross-boundary, versioned, immutable, past-tense) — with synchronous request/response through an approved API contract reserved for interactions that genuinely need an immediate answer.

### How It Works at Strategy Level
| Interaction type | Mechanism | Source |
|---|---|---|
| In-process calls within one Bounded Context | Direct method call, no event needed | Constitution §12 (Domain Events stay inside a Bounded Context) |
| Immediate-answer cross-Module need (e.g., "is this permission granted") | Synchronous API call through an approved contract | ADR-0004; Constitution §5 |
| Cross-Module side effect, no immediate answer needed | Integration Event (RabbitMQ, E7), versioned, at-least-once delivery, idempotent consumers | ADR-0004; Constitution §12, §13, §34 |
| Cross-Bounded-Context integration with an external Engine's foreign model | Anti-Corruption Layer / Adapter Boundary translation | Constitution §6; `docs/reuse/MASTER_ENGINE_CATALOG.md` |
| Device-originated data reaching the business Core | Integration Event via the Device Integration Gateway's Anti-Corruption Layer, provenance preserved | ADR-0006; Constitution §24 |
| Partner integration | API contract (candidate, 0 designed today) | Wave 2 §7, §11; `21-INTEGRATIONS.md` |

### Rationale
ADR-0004's Alternatives Considered rejected synchronous-only calls (tight coupling, undermines Module Dependency Rules) and shared-database triggers/polling (conflicts with Schema per Module, hides the contract inside database internals). Event-Driven Integration matches the platform's stated API-First/Event-Driven direction (`vision.md`) while still allowing synchronous calls where genuinely needed — the ADR does not claim every interaction is asynchronous.

### Consequences and Trade-offs
Positive: modules evolve and fail independently for side effects; the event stream is a natural audit/traceability aid. Negative: requires designing for eventual consistency (a genuine mental-model cost) and idempotent, redelivery-tolerant consumers (Constitution §34).

### Guardrails
**Not every communication is asynchronous** — this Wave does not claim that. **CQRS and Event Sourcing are not Accepted** anywhere in this repository; both sit on the Architecture Radar's "Assess" tier (Constitution §54), each requiring its own measured trigger (Constitution §55) before adoption — this Wave records them as `Assess`, not as decided architecture. No Kafka/Topic/Queue schema is designed here (that is `docs/api-platform/18` / later-Wave work); RabbitMQ (E7) is the ratified transport Engine, cited not re-selected.

### Deferred Detail / Owning Wave
Topic/queue naming, event schema definitions, per-Module Event Catalog entries: `docs/api-platform/18-ASYNCAPI-EVENTS.md` (already exists, referenced) and Wave 4/5.

### Traceability
ADR-0004; Constitution §12–13, §34; `18-ASYNCAPI-EVENTS.md`.

### Status Classification
**Accepted Decision Synthesis**, with CQRS/Event Sourcing explicitly classified **Deferred Design Detail (Assess tier, not Accepted)**.

## 10. API and Interoperability Strategy

### Driver / Problem
Multiple client surfaces (Web Platform, Patient App, Sample Collector App), future Partner integrations, and external Engines all need a consistent, governed way to reach the platform without exposing internal schema or any Engine's native surface.

### Accepted Strategy
A single, unified, API-First backend (no Portal-specific fork) organized across a layered model, fronted by an approved Edge Gateway (Kong Gateway, D-44), with every external Engine wrapped by the platform's own contract and an Anti-Corruption Layer, contract-first governance for both REST (OpenAPI 3.1.x) and events (AsyncAPI 3.x), and Public API deliberately deferred (0 designed).

### How It Works at Strategy Level
"One backend, many front doors" (`01-API-VISION.md`) — a single, versioned API surface serves web Portals, mobile clients, Admin Dashboards, and (not yet designed) Partner/Public consumers. API surfaces are classified Internal, External (Portal-facing), Partner, Public, Admin, and Integration (`03-API-DOMAIN-INVENTORY.md`) — a classification scheme, not a claim that every classification is equally built today: 28 domain entries carry at least an Internal surface, 21 an External surface, 6 are Partner candidates (0 designed), and Public is explicitly 0 by deliberate non-decision. Kong Gateway is the single entry point for External/Partner/Public/Admin traffic (never Internal traffic) and owns TLS termination, authentication-token validation, coarse Role-level authorization, routing, rate limiting, and protocol/version transformation — it holds no business logic and never performs Sensitive-Operation/Human-in-the-Loop gating, which stays at each Module's own Aggregate layer (`10-API-GATEWAY.md`). This is the platform's **two-Policy-Enforcement-Point pattern**: a coarse, Role-level PEP at the Edge Gateway, and a fine, Data-Scope-level PEP at each Module boundary — neither substitutes for the other, directly extending Constitution §21's "authorization is never UI-only" rule one layer further inward (`09-AUTHORIZATION.md`).

### Rationale
Contract-first (`16-CONTRACT-FIRST.md`) makes the contract, not the running service, the source of truth — matching the platform's API-First architectural principle (Constitution, Consolidated Accepted Decisions appendix). Kong Gateway was selected via the Open Questions Resolution phase (D-44) for its Apache-2.0 license (matching this repository's consistently demonstrated license preference), mature OIDC/JWT/rate-limiting plugin ecosystem, and self-hostability (ADR-0009).

### Consequences and Trade-offs
Positive: one governed entry point simplifies cross-cutting concerns (auth, rate limiting, correlation IDs) without duplicating them per Module. Negative: the Gateway is a critical dependency for every external-facing call; a two-PEP model requires both layers to stay correctly synchronized, not just one.

### Guardrails
No endpoint path, payload schema, OpenAPI document, authentication flow detail, version number, rate-limit number, error-body shape, or SDK is designed in this Wave — all are already-existing `docs/api-platform/` content, cited, not re-authored, or Wave-4-and-later work. The Gateway responsibility list above (TLS termination, token validation, coarse authorization, routing, rate limiting, protocol/version transformation) is **quoted from `10-API-GATEWAY.md`'s own existing "Gateway Responsibilities Summary" table, not new component design by this Wave** — it is restated at this level of detail only because it directly supports the two-PEP authorization pattern (§12); no Container or Component diagram results from it, and no responsibility not already in that source table is added here. **Kong Gateway is an approved Version 1 product selection, not subject to architectural re-evaluation during SAD authoring** (`22-ARCHITECTURE-BASELINE-FREEZE.md` Governance Statement) — this Wave treats it as fixed input.

**FHIR version — Source Precedence applied.** `docs/api-platform/03-API-DOMAIN-INVENTORY.md` and `30-ROADMAP.md` still read "FHIR version not pinned... blocked on R-06" — this predates the Open Questions Resolution phase (2026-07-18). The current, governing status is **FHIR R4, formally pinned** (D-43; R-06 Closed; Technology Baseline R1), exactly the same staleness pattern Wave 2 §7/§11 already found and corrected for notification channels and legacy migration. This Wave states the current status and cites where the stale text originated, consistent with that established precedent — it does not edit `docs/api-platform/` itself (out of this Wave's scope-lock).

### Deferred Detail / Owning Wave
Endpoint/payload/schema design, authentication flow detail, SDK generation output: already covered at the appropriate depth in `docs/api-platform/`, cross-referenced by Wave 4 and Wave 10.

### Traceability
`01-API-VISION.md`, `02-API-FIRST-ARCHITECTURE.md`, `03-API-DOMAIN-INVENTORY.md`, `09-AUTHORIZATION.md`, `10-API-GATEWAY.md`, `16-CONTRACT-FIRST.md`, `17-OPENAPI-GOVERNANCE.md`, `18-ASYNCAPI-EVENTS.md`, `20-SDK-STRATEGY.md`, `21-INTEGRATIONS.md`, `22-DEVELOPER-PORTAL.md`, `25-MONETIZATION.md`; D-43, D-44, D-46, D-47; `02-TECHNOLOGY-BASELINE.md` E22 (Kong Gateway); ADR-0006, ADR-0007; Wave 2 §7, §11.

### Status Classification
**Accepted Decision Synthesis**, with the FHIR-version status corrected per Source Precedence (Constitution/certification sources over stale `docs/api-platform/` text) and Public API explicitly **Open Dependency (deliberate non-decision)**.

## 11. Data and Persistence Strategy

### Driver / Problem
Each Module needs a data-ownership model that preserves Modular Monolith boundaries, supports the Hybrid Tenant Isolation model, and rests on a formally chosen relational engine rather than an implicit assumption.

### Accepted Strategy
**PostgreSQL** as the primary transactional relational engine (ADR-0013); **Schema per Module** ownership (ADR-0003) — no cross-module SQL joins or writes; **PostgreSQL Row-Level Security + tenant-ID column** as the shared-tier partitioning default (D-42, R4), with dedicated database/deployment for the Dedicated tier (ADR-0005).

### How It Works at Strategy Level
Every Module owns a distinct schema (or clearly namespaced table set) and its own migrations; another Module's data is reached only through that Module's API, Domain/Integration Events, or an explicitly approved Read Model (Constitution §16). Within the shared tier, every tenant-scoped query is additionally scoped by RLS + tenant-ID at the database layer, not only in application code. Transactions are scoped to a single Module's ownership boundary; cross-boundary consistency between Modules is eventual, achieved through the Integration Event mechanism (§9), not distributed transactions. Audit/provenance data is stewarded by the platform via immudb (E4), a tamper-evident store distinct from ordinary operational data (Constitution §23). Search, analytics, file, and document capability are served by specialized Engines (Apache Superset for analytics, `pgvector` for vector search inside PostgreSQL itself, Alfresco for document management) rather than folding those concerns into every Module's own transactional schema.

### Rationale
ADR-0013's own Context section establishes that RLS (D-42) and `pgvector` (Technology Baseline L1) already presuppose PostgreSQL specifically — this ADR "does not select a new technology, it names the technology every existing decision already depends on." Schema per Module (ADR-0003) was chosen over a fully shared schema (destroys module ownership) and Database per Module from day one (unjustified operational cost before a measured need exists).

### Consequences and Trade-offs
Positive: tenant isolation is enforced at the database layer, not only in application code; a Module can move to a dedicated database later as a pure deployment change, since it never depended on cross-schema access. Negative: cross-Module reporting cannot use simple SQL joins — it must go through approved Read Models or the Analytics Platform; RLS-based co-location makes selective single-tenant restore architecturally harder for the shared tier specifically (ADR-0014's own "Pending Workload Evidence" note on this point).

### Guardrails
No table, column, index, partitioning scheme, replication topology, retention number, or detailed transaction workflow is designed here — Wave 4 and Wave 6 territory. "Not every workload must be stored in PostgreSQL" and "not every Module shares one physical database instance" are ADR-0013's own explicit scope-limits, restated, not narrowed, here.

### Deferred Detail / Owning Wave
Schema design, table/column definitions, index strategy, replication/partitioning topology: Wave 4 (Building Block View) and Wave 6 (Deployment View).

### Traceability
ADR-0003, ADR-0005, ADR-0013, ADR-0014; D-42, D-56 (PostgreSQL formally adopted as the primary relational database engine); `02-TECHNOLOGY-BASELINE.md` R4, L1, E4, E10, E11, E24 (PostgreSQL — the section's own primary Engine, per ADR-0013); Wave 2 §12.

### Status Classification
**Accepted Decision Synthesis** (engine and ownership pattern); **Frozen Baseline Input** (RLS/tenant-ID as the shared-tier default, D-42).

## 12. Multi-Tenancy, Identity and Access Strategy

### Driver / Problem
Multiple client surfaces and user types must reach the correct Portal/Dashboard with backend-enforced, fine-grained access that respects Tenant/Organization/Branch boundaries, without ever relying on the UI as a control.

### Accepted Strategy
**Hybrid Tenant Isolation** (ADR-0005) plus **Unified Login and Policy-Based Access** (ADR-0008): one authentication entry point across all clients, backend-enforced and policy-based authorization evaluating Role, Permission, Policy, Data Scope, Organization, Branch, Resource Ownership, and Consent for every state-changing and sensitive-read operation.

### How It Works at Strategy Level
Keycloak (E1) is the ratified Identity Engine; OPA (E2) is the ratified Policy Engine — together realizing ADR-0008's mechanism, per the Technology Baseline's own Owner mapping (Identity and Access). Authorization is enforced at (at least) two layers, consistent with §10's two-PEP pattern: a coarse Role-level check at the Edge Gateway, and a fine Data-Scope-level check at each Module's own boundary — client-supplied role/permission claims are never trusted without backend verification (Constitution §20). Least Privilege and Deny by Default apply platform-wide; sensitive operations require elevated controls, and Break-Glass access is exceptional, time-limited, justified, and fully audited (Constitution §21).

### Rationale
ADR-0008's Alternatives Considered rejected per-client-surface identity systems (contradicts the explicit Unified Login requirement) and UI-enforced visibility as a primary control (explicitly forbidden — trivially bypassed via direct API calls). Plain RBAC was also rejected as insufficient for the platform's Organization/Branch/Resource-Ownership/Consent granularity needs.

### Consequences and Trade-offs
Positive: one place to reason about "can this user do this action"; UI-hiding-as-security is structurally excluded by design. Negative: more upfront design work (Policy + Data Scope + Resource Ownership + Consent evaluation per sensitive operation) than a simple role check; Unified Login/Backend Platform becomes a critical dependency for every client.

### Guardrails
No RBAC/ABAC policy model detail, token content, login-flow sequence, tenant-provisioning procedure, RLS policy implementation, break-glass UX, or delegated-administration detail is designed here — all Wave 8 territory. This Wave does not claim client-side authorization is ever sufficient anywhere in the platform.

### Deferred Detail / Owning Wave
Policy model detail, token contents, login flows, tenant provisioning, RLS policy implementation, break-glass mechanics, delegated administration: Wave 8 (Multi-Tenancy, Identity & Access Governance).

### Traceability
ADR-0005, ADR-0008; Constitution §18–22; `02-TECHNOLOGY-BASELINE.md` E1, E2; `08-AUTHENTICATION.md`, `09-AUTHORIZATION.md`; Wave 2 §12.

### Status Classification
**Accepted Decision Synthesis.**

## 13. Open-Source Reuse and Engine Integration Strategy

### Driver / Problem
Most of the platform's cross-cutting and Supporting/Generic capability (identity, policy, HR/payroll, ERP, insurance administration, scheduling, notifications) is not this platform's differentiator; building it all in-house would divert investment away from the Core Domain (§4) without a corresponding competitive gain.

### Accepted Strategy
Mature open-source Engines are reused behind the platform's own adapter/contract boundary wherever they fit a Supporting or Generic capability, evaluated on an evidence-based, documented scoring model — never a GitHub-star count — with the Core Domain explicitly protected from wholesale displacement. A Technology Baseline of **24 Engines, 4 Libraries, 5 Reference Standards (33 entries)** is frozen as the platform's adopted-technology input, each entry's Approved / Conditionally Approved / License-Dependency status preserved individually.

### How It Works at Strategy Level
Every adopted Engine remains behind the platform's own API and, where it touches a Bounded Context's domain model, an Anti-Corruption Layer (documented in the reuse research as an "Adapter Boundary," e.g., Keycloak wrapped inside Identity and Access's own boundary, `docs/reuse/MASTER_ENGINE_CATALOG.md`). The owning Bounded Context or Module remains the accountable "Single Adoption Point" for a capability even when an Engine implements it — the Engine is a replaceable implementation detail, never the architecture itself (`docs/reuse/MASTER_DEPENDENCY_MATRIX.md`: "OpenBoxes is the platform's single stock-management Adoption Point"; Module 12 "owns the catalog list price... ERPNext Pricing Rules apply commercial discounts on top, a distinct layer, not a duplicate"). Where a whole-system Engine was evaluated against a Core-Domain-adjacent Module (Patient Management, Diagnostic Ordering, Specimen Operations, Laboratory Execution, Result Verification and Reporting), it was rejected for wholesale adoption specifically to protect the `TestResult` Aggregate chain — the one exception, openIMIS for Insurance and Corporate Contracts, was judged correctly outside that chain, not a Core Domain leak (§7 above; `docs/architecture-review/10-ADR-REVIEW.md`).

Status preserved distinctly, not flattened to a uniform "adopted":

| Category | Count | Examples |
|---|---|---|
| Fully Approved (original EARB freeze — Enterprise Architecture/Adoption Review Board, the governance function that ratified the Technology Baseline, Constitution §57) | 19 | Keycloak, OPA, RabbitMQ, ERPNext, Frappe HR, Kill Bill |
| Conditionally Approved (original freeze) | 2 | Eramba Community (implementation due diligence gate before production); Mirth Connect (frozen-release, migration path tracked, R-02) |
| Fully Approved (added 2026-07-18) | 3 | Kong Gateway, OpenBao, PostgreSQL |
| Carrying an unresolved License/Legal dependency (subset of the above, not a separate count) | 7 | Cal.com, Atlas CMMS, openIMIS, Frappe Helpdesk, Frappe CRM (5, AGPL-3.0, R-04); Novu, Documenso (2, unconfirmed license, R-07) — 7 distinct Engines total, no name counted twice |

**A License/Legal Dependency does not mean an Engine is rejected, and a Frozen Baseline does not mean every Engine's due diligence is complete** — both are preserved, distinct states (Wave 2 §3, restated).

**Forking**: available as a Final Decision category (`CONTROLLED FORK`) but never selected across the 106-Feature reuse program — an unused exception path, not a default (`docs/reuse/MASTER_COMPLETION_REPORT.md`, "Decision Taxonomy Applied"). No fork of an adopted Engine is planned by this Wave.

### Rationale
Reuse-before-build for Supporting/Generic capability is the direct architectural application of the `domain-driven-design` skill's Strategic Design/Distillation practice (§4, §7, §25): the Core Domain earns deepest in-house investment; Supporting and Generic subdomains are built or bought according to fit, never over-engineered. The reuse program's own scoring model (Architecture 15%, Security 15%, License 10%, Testing/CI 10%, Community Health 10%, Enterprise Adoption 10%, Healthcare Suitability 10%, Documentation 5%, Extensibility 5%, Upgradeability 5%, Vendor Independence 5% — `docs/reuse/MASTER_COMPARISON_MATRIX.md`) is the evidentiary basis for every adoption, not GitHub popularity.

### Consequences and Trade-offs
Positive: 106 of 106 build-vs-buy Features resolved with 0 architectural blockers; deepest engineering investment concentrated on the Core Domain rather than spread across commodity capability. Negative: 7 Engines carry a genuine AGPL-3.0/unconfirmed-license exposure requiring formal legal review (R-04, R-07) before production commitment on any API Product built atop them; the platform's broadest single-Engine footprint (ERPNext, 5 Modules) is a concentration risk requiring exit-strategy attention (R-03, R-08).

### Guardrails
**"All 24 Engines are fully approved" is not a statement this Wave makes anywhere** — the table above is the only accurate summary. No new Engine is selected, compared, or rejected in this Wave; no existing Engine's status is upgraded or downgraded. Kong Gateway and OpenBao are approved Version 1 selections, not subject to re-evaluation during SAD authoring (`22-ARCHITECTURE-BASELINE-FREEZE.md`). Eramba Community is not subject to re-evaluation during SAD authoring — only implementation due diligence remains (`26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`).

### Deferred Detail / Owning Wave
Per-Engine Exit Strategy procedures for the 7 Tier-1 Engines (R-08): explicit SAD deliverable, target Wave 12 (Risks, Technical Debt & Evolution). AGPL-3.0 formal legal review outcome (R-04): outside architectural authority, tracked as an Open Dependency (§22).

### Traceability
`02-TECHNOLOGY-BASELINE.md`; `12-DECISION-FREEZE.md`; `22-ARCHITECTURE-BASELINE-FREEZE.md`; `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`; `docs/reuse/MASTER_EXECUTIVE_SUMMARY.md`, `MASTER_BUILD_VS_BUY_MATRIX.md`, `MASTER_COMPARISON_MATRIX.md`, `MASTER_ENGINE_CATALOG.md`, `MASTER_DEPENDENCY_MATRIX.md`, `MASTER_LICENSE_MATRIX.md`, `MASTER_COMPLETION_REPORT.md`; `docs/architecture-review/10-ADR-REVIEW.md`; R-01 through R-08.

### Status Classification
**Accepted Decision Synthesis** (reuse pattern, Technology Baseline); **Open Dependency** (AGPL legal review, exit-strategy procedures).

## 14. Device Integration Strategy

### Driver / Problem
Device communication is protocol-heavy, vendor-specific, and prone to malformed/partial data; placing it directly inside a business Module would couple business rules to device specifics and risk core-data corruption from device-side failures.

### Accepted Strategy
An **independent Device Integration Gateway** (one of the 8 Independent Components), using Vendor Adapters and Protocol Adapters outside the business Core, translating device data into Integration Events consumed through an Anti-Corruption Layer, with provenance retained on every imported result and failures isolated rather than silently corrupting core data.

### How It Works at Strategy Level
The Gateway must be able to support HL7, HL7 v2, FHIR, ASTM, TCP/IP, Serial Communication, File-Based Integration, and Vendor APIs over time — architecture must not preclude any of these, though not all are necessarily implemented in v1 (Constitution §24). Mirth Connect (E6) is the ratified integration Engine, with Apache Camel documented as the evaluated fallback given Mirth's frozen-release risk (R-02). Every imported result carries source and provenance (which device, which adapter, when, raw-payload reference) permanently. A device/adapter failure is isolated, logged, and surfaced for review — never silently swallowed, never allowed to write partial/invalid state into the domain (Constitution §24).

### Rationale
ADR-0006's Alternatives Considered rejected embedding device adapters inside the Laboratory Module (couples business logic to protocol specifics, risks malformed-payload corruption of verified state) and a single unstructured "integration" module for all external systems (device integration's distinct reliability/provenance needs warrant a dedicated, named component).

### Consequences and Trade-offs
Positive: new vendors/protocols are added at the Gateway without touching business Module logic; core data is protected from malformed device payloads by construction. Negative: an operationally independent component to run/monitor from v1; an Anti-Corruption Layer must be designed and maintained per vendor/protocol.

### Guardrails
No protocol implementation, port configuration, device driver, message-parsing algorithm, retry algorithm, or device inventory is designed here — Wave 9 territory. Business/domain logic (e.g., result interpretation) may never live inside a device adapter (Constitution §24, restated).

### Deferred Detail / Owning Wave
Protocol implementation detail, device driver specifics, retry/parsing algorithms: Wave 9 (AI Governance, Device Integration & Other Cross-Cutting Concerns).

### Traceability
ADR-0006; Constitution §24; `02-TECHNOLOGY-BASELINE.md` E6; R-02; Wave 2 §7, §11.

### Status Classification
**Accepted Decision Synthesis.**

## 15. AI Integration and Governance Strategy

### Driver / Problem
The platform is directionally "AI-Ready," but AI must never issue a final, unreviewed medical decision — a constraint that cannot be enforced by policy alone across many independently-built AI-assisted features.

### Accepted Strategy
An **independent, governed AI Gateway** (one of the 8 Independent Components) supporting summarization, patient-friendly explanations, pattern detection, anomaly detection, search, operational assistance, and clinical decision *support* — never final medical approval — with mandatory Human-in-the-Loop before any sensitive clinical action is finalized, and every AI action logged and auditable.

### How It Works at Strategy Level
Portkey Gateway (E9) is the ratified LLM Gateway Engine, wrapping whichever underlying model provider is used — no specific provider is named or selected by any source reviewed, and none is invented here (Wave 2 §7). AI output reaching a "final" sensitive-clinical state without a human-approval step must be structurally blocked, not merely policy-discouraged (Constitution §28). Sending sensitive information to an external AI provider requires an approved policy and controls (e.g., data minimization) to exist first — never a default-on data flow.

### Rationale
ADR-0007's Alternatives Considered rejected embedding AI directly per-Module (makes uniform governance/audit/Human-in-the-Loop enforcement impossible) and fully autonomous AI action on medical data with exception-only review (a direct violation of the platform's own explicit constraint, restated in Wave 1 §7 constraint #6).

### Consequences and Trade-offs
Positive: one place to enforce AI governance controls; a clear, auditable boundary between "AI suggested" and "human approved." Negative: every sensitive AI-assisted feature requires building/using the Human-in-the-Loop review step, extra product/UX work versus a naive "just show the AI output" approach.

### Guardrails
No prompt template, approval-UI design, model-routing algorithm, evaluation metric, or specific provider/model selection is designed here. **"AI output is not automatically authoritative clinical truth"** is restated, not weakened, from Constitution §28. No clinical AI use case beyond the 7 already-candidate use cases (Wave 10 territory) is asserted as Accepted here.

### Deferred Detail / Owning Wave
Approval-workflow UX, prompt/model routing, evaluation metrics, per-use-case clinical review: Wave 9 (AI Governance, Device Integration & Other Cross-Cutting Concerns).

### Traceability
ADR-0007; Constitution §28; `02-TECHNOLOGY-BASELINE.md` E9; Wave 1 §7, §8.

### Status Classification
**Accepted Decision Synthesis.**

## 16. Deployment Portability and Operational Strategy

### Driver / Problem
Tenants range from SaaS-comfortable organizations to large/regulated organizations that may require on-premise or hybrid deployment; the architecture must not foreclose either without becoming cloud-provider-locked.

### Accepted Strategy
**SaaS First, On-Premise Ready, Hybrid Ready** (ADR-0009): the primary delivery model is SaaS, the same logical architecture must remain deployable on-premise or in a hybrid mode, the cloud provider must remain replaceable where practical, and data residency must be configurable per market.

### How It Works at Strategy Level
This is a readiness commitment at the architecture level, not a claim that on-premise packaging is fully built in v1 — Domain Core logic (§8) is kept isolated from any specific infrastructure dependency by construction (Ports and Adapters), which is what makes multi-mode deployment possible without a redesign per mode. Configuration and infrastructure concerns are isolated from Domain Core (Constitution §48, Configuration Management). Shared Platform/Tenant operational responsibility exists across all three modes, with the exact split for On-Premise/Hybrid a commercial/contractual matter (ADR-0014's "Relationship Between SaaS, On-Premise, and Hybrid Deployment Modes" section, restated).

### Rationale
ADR-0009's Alternatives Considered rejected SaaS-only (blocks large/regulated tenants needing on-premise/hybrid, an explicit user requirement) and on-premise-first (slows the common-case tenant onboarding path) and cloud-provider-locked design (forecloses replaceability).

### Consequences and Trade-offs
Positive: the common case (SaaS) is optimized without closing the door on regulated tenants; avoids deep cloud-provider lock-in. Negative: "replaceable where practical" and multi-mode support add architectural discipline overhead versus a single-cloud SaaS-only design; on-premise/hybrid readiness must be validated even before a concrete on-premise tenant exists.

### Guardrails
**No cloud provider, region, availability zone, Kubernetes/orchestration choice, VM sizing, or network topology is selected in this Wave** — all explicitly Wave 6 (Deployment View) and, for numeric DR targets, Wave 11/ADR-0014's own Pending structure. This Wave does not claim the architecture "guarantees" availability or scalability at any level — no such claim exists in any source reviewed.

### Deferred Detail / Owning Wave
Cloud provider selection, container orchestration, network topology, DR topology and numeric RPO/RTO: Wave 6 (Deployment View) and Wave 11 (Quality Requirements & Quality Scenarios).

### Traceability
ADR-0009, ADR-0014; Constitution §48; Wave 2 §3, §5.

### Status Classification
**Accepted Decision Synthesis** (readiness commitment); **Deferred Design Detail** (concrete topology).

## 17. Auditability, Observability and Reliability Direction

### Driver / Problem
A healthcare/billing platform cannot treat an ambiguous failure or an unaudited sensitive action as acceptable; distinguishing "is this module healthy" from "what happened for this sensitive action" requires two structurally separate signal types.

### Accepted Strategy
**Audit is a platform concern, structurally distinct from operational observability** (Constitution §23, §33): every sensitive action produces an immutable Audit Event (immudb-backed, tamper-evident); every Module exposes Logs, Metrics, and Health as three distinct signal types; failure isolation is achieved through the Independent Components' own boundary (Device Gateway, AI Gateway) rather than allowing a dependency failure to corrupt core state; long-running/deferred work runs as an explicit, trackable Background Job.

### How It Works at Strategy Level
Audit Events are immutable, retained independently of the business record they describe, and never mutated or deleted as part of any normal workflow (Constitution §23). Operational logs are structured, Correlation-ID-propagating, and never carry medical data or secrets in plaintext (Constitution §48, Logging Policy) — the same Correlation ID (or a documented causation chain) is expected to appear across every Module/Event a single business operation touches, so a cross-Module flow can be traced end-to-end even before a specific tracing backend is chosen. A dependency (device, external AI provider, external API partner, another Module) failing must degrade gracefully, never silently corrupt data or leave a workflow undefined (Constitution §34).

### Rationale
This direction is the direct restatement of already-Accepted Constitution rules (§23, §33, §34, §48) applied at the strategy level — no new principle is introduced. `docs/api-platform/27-OBSERVABILITY.md` already defines the metrics/logging/tracing architecture with Apache Superset (E10) for dashboards; this Wave cites it rather than re-deriving it.

### Consequences and Trade-offs
Positive: audit and operational concerns never get conflated into one undifferentiated log stream, keeping both reliable. Negative: requires disciplined instrumentation per Module from day one (three distinct signal types, not "we have some console output").

### Guardrails
**No numeric SLO, error-rate target, or availability commitment is fabricated here** — Constitution §51 keeps these Draft pending real usage data (Open Question #4), and this Wave does not narrow that gap. Strategic direction here is distinct from: detailed security/audit controls (Wave 7), Quality Scenarios with numeric targets (Wave 11), and Risk Treatment (Wave 12) — this Wave states only the direction those later Waves elaborate.

### Deferred Detail / Owning Wave
Detailed security/audit controls: Wave 7. Quality Scenarios with numeric targets: Wave 11. Risk treatment: Wave 12.

### Traceability
Constitution §23, §33, §34, §48; `27-OBSERVABILITY.md`; `02-TECHNOLOGY-BASELINE.md` E4, E10.

### Status Classification
**Accepted Decision Synthesis** (direction); **Deferred Design Detail** (numeric targets, detailed controls).

## 18. Evolution and Selective Extraction Strategy

### Driver / Problem
The platform must be able to evolve toward higher scale or different operational needs later without either (a) having over-built distributed-systems infrastructure prematurely, or (b) being structurally unable to extract a Module when a real need arises.

### Accepted Strategy
Start modular (§6); measure coupling, load, team, and operational needs; extract, add CQRS, add Event Sourcing, add a dedicated Search/Cache/Analytics component, or split a Module's database only when a documented, measurable trigger fires (Constitution §55) — never in anticipation, and never merely because a pattern is "best practice." Selective Service Extraction of any Module requires its own ADR (ADR-0001's process).

### How It Works at Strategy Level
| Evolution | Trigger type required | Not a valid trigger |
|---|---|---|
| Split a Module into an independent service | Measured, sustained operational need (scaling, deployment cadence, team-boundary conflict), documented in a new ADR | "Microservices are best practice"; anticipated future scale |
| Split a Module's database | Extraction (above), or a large/regulated tenant's dedicated-database requirement (ADR-0005) | Convenience; avoiding a cross-schema query that should go through a contract |
| Add CQRS | Measured, divergent read/write load for that specific Module | "CQRS is a best practice for complex domains" without measured divergence |
| Add Event Sourcing | A concrete, unmet requirement for full historical reconstruction Audit Events cannot satisfy | General auditability needs (already satisfied by Constitution §23) |
| Add a dedicated Search Service | Query/search needs measurably exceed what the owning Module's data store can serve | Preemptive addition "in case we need search later" |
| Add a dedicated Cache layer | Measured latency/load data (once Non-Functional Budgets, §51, leave Draft) showing a path exceeds budget | Guessing that caching "will probably help" |

*(Table restates Constitution §55 verbatim in substance; no new row or threshold is introduced.)*

### Rationale
Directly implements Core Value "Evidence over imagination" (Constitution §4) and the Architecture Radar's "Assess" tier for CQRS, Event Sourcing, a dedicated Search Service, a dedicated Cache layer, and Sagas/process managers (Constitution §54) — each explicitly not a default, each requiring a Migration Trigger before adoption.

### Consequences and Trade-offs
Positive: engineering effort is spent where a real, measured need exists, not on speculative infrastructure. Negative: some capability genuinely needed later (e.g., a dedicated cache) is not available until the trigger fires and the work is done — a deliberate, accepted lag, not an oversight.

### Guardrails
**No numeric threshold is invented for any trigger above** — Constitution §55 itself withholds numbers pending real scale data (Open Question #4), and this Wave does not narrow that gap. No extraction candidate or Search/Cache/Analytics addition is declared "planned" or "next" by this Wave — none is Accepted today.

### Deferred Detail / Owning Wave
Actual extraction/CQRS/Event-Sourcing/Search/Cache decisions, once and if a trigger fires: a future ADR, at the time the trigger is measured — not this Wave, not any fixed later Wave, since it is evidence-triggered rather than schedule-triggered.

### Traceability
Constitution §4, §54, §55; ADR-0001 (Revisit Triggers).

### Status Classification
**Accepted Decision Synthesis** (the trigger discipline itself); every specific evolution (extraction, CQRS, Event Sourcing, dedicated Search/Cache) is **Deferred Design Detail**, contingent on a future measured trigger, not Accepted architecture today.

## 19. Strategy Trade-offs

| Trade-off | Benefit | Cost | Risk | Mitigation Already Accepted | Residual/Open Issue | Source |
|---|---|---|---|---|---|---|
| Modular Monolith speed vs. internal discipline | Fast iteration, low operational overhead while domain is discovered | Requires sustained architecture-test discipline to prevent boundary erosion | Boundary erosion into a Big Ball of Mud if tests lapse | Constitution §9, §49 (Module Isolation/Dependency Direction Fitness Functions) | Fitness Function automation itself is a Wave 4/implementation task, not yet built | ADR-0001 |
| Independent components vs. operational complexity | Protocol isolation, governed external calls, variable-load isolation | 8 additional operationally independent components to run/monitor from v1 | Coordination overhead across more deployables than a pure monolith | Constitution §11 (contract-only consumption) | Actual operational tooling/monitoring maturity is Wave 6/9 work | Constitution §11 |
| OSS reuse vs. licensing/vendor risk | 106/106 Features resolved without building commodity capability from scratch | 7 Engines carry AGPL-3.0/unconfirmed-license exposure | Legal exposure if network-use clauses apply; vendor abandonment (Mirth Connect frozen-release) | Documented Replacement Candidates per Engine; R-08 Resolution Gate | Formal legal opinion (R-04, R-07) and Exit Strategy procedures (R-08) both still owed | `02-TECHNOLOGY-BASELINE.md`; R-01–R-08 |
| Event-driven decoupling vs. eventual consistency | Independent Module evolution/failure; natural audit trail | Consumers must be idempotent, redelivery-tolerant; eventual-consistency mental model | Ordering/duplicate-delivery bugs if idempotency is skipped | Constitution §34 (Reliability and Resilience Rules) | Concrete idempotency-key design is Wave 4/5 work | ADR-0004 |
| Multi-mode deployment readiness vs. configuration complexity | No tenant is turned away on deployment-mode grounds | Architectural discipline overhead avoiding cloud-provider lock-in | Silent SaaS-only coupling creeping in via a convenient managed-service dependency | Architecture review checklist at new-dependency adoption time (ADR-0009 Verification) | Concrete topology per mode is Wave 6 work | ADR-0009 |
| Strong governance vs. delivery overhead | Predictable, auditable decisions; no silent architectural drift | Every significant decision needs an ADR; every Wave needs explicit acceptance before the next begins | Governance becomes a bottleneck if the ARB (today: one person) is unavailable | Constitution §57 Decision Types table scopes exactly which decisions need this weight | Constitution §62 already logs this as an open Governance Gap (single point of authority, no succession rule) | Constitution §57, §62 |

No mitigation listed above is a decision this Wave invents — each cites the Constitution section, ADR, or Risk Register entry that already establishes it.

## 20. Rejected or Deferred Alternatives

| Alternative | Source | Why rejected/deferred | Permanently rejected or revisit-able | Revisit trigger |
|---|---|---|---|---|
| Microservices First (from day one) | ADR-0001 | Distributed-systems cost paid before domain/team structure justify it | Revisit-able, per-Module | Measured, sustained operational need for independent scaling/deployment/team autonomy (ADR-0001 Revisit Triggers) |
| Shared database, no per-Module ownership boundary | ADR-0003 | Destroys module ownership; guarantees Distributed-Monolith-in-waiting | Effectively permanent as a platform-wide default | None named — this is a structural rule, not a scheduled revisit |
| Direct native Engine exposure to Portal/Partner/Public | `01-API-VISION.md`, `02-API-FIRST-ARCHITECTURE.md` | Couples the platform's public contract to vendor-specific schemas; forecloses replaceability | Permanently rejected as a default | An ACL-preserving exception would itself require architecture review, not a default path |
| Direct device integration into the business Core | ADR-0006 | Couples business logic to protocol/vendor specifics; risks core-data corruption from malformed payloads | Permanently rejected | A specific protocol/vendor proving the Gateway abstraction insufficient prompts a scoped refinement, not a reversal |
| Direct model-provider access from Core or Portals | ADR-0007 | Makes uniform AI governance/Human-in-the-Loop enforcement impossible | Permanently rejected | None named — mandatory-HITL core is not revisit-able without a superseding ADR |
| Portal-specific backend forks | `01-API-VISION.md` Goal 1 | Contradicts the "one backend, many front doors" principle | Not currently revisit-able | Not named in any source reviewed |
| Public API now (general-purpose developer access) | `03-API-DOMAIN-INVENTORY.md`, `33-PART2-EXECUTIVE-SUMMARY.md` | A business Decision not yet made, outside architectural authority | Revisit-able | A future, explicit business Decision to open Public API access |
| Fully shared tenant isolation only (no dedicated tier) | ADR-0005 | Cannot satisfy large/regulated tenants' contractual/regulatory isolation needs | Revisit-able | A regulatory requirement the two-tier model cannot satisfy for a given market |
| Dedicated database/deployment per tenant, always | ADR-0005 | Operationally expensive and unjustified for small tenants by default | Revisit-able | Measured operational cost data prompting a tier-promotion-path refinement |

No alternative above was invented to fill this table — each is drawn directly from an ADR's own Alternatives Considered section or an equivalent already-Accepted source's explicit rejection.

## 21. Explicit Non-Decisions

What Wave 3 does **not** decide, listed explicitly per the governing instruction, none silently resolved elsewhere in this document:

- The 28 Bounded Contexts' mapping to implementation Modules (if a 1:1 mapping holds at all).
- Containers, Components, or any deployable-unit count beyond the 8 already-Accepted Independent Components.
- A per-context inventory of which interactions are synchronous vs. asynchronous (§9 states the general rule only).
- Runtime orchestration or sequence design for any workflow.
- Deployment topology (cloud provider, region, orchestration, network zones).
- Security control design (STRIDE analysis, specific mitigations).
- RBAC/ABAC policy-model detail, token contents, or login-flow sequences.
- AI approval-workflow UX or model-routing detail.
- Device protocol implementation detail.
- Any numeric quality target (latency, throughput, availability, RPO, RTO, error rate).
- Detailed risk-treatment plans for any Risk Register entry.
- Partner commercial terms for any of the 6 Partner API candidates.
- Selection of any specific vendor not already named in the Technology Baseline.
- Any Selective Service Extraction candidate — none is declared "next" or "planned" by this Wave.
- Whether the Specimen Management alternative supersedes ADR-0011's Core Domain framing.
- Whether the Specimen Operations/Laboratory Execution Bounded Context split should be reconsidered.

## 22. Open Dependencies

| Item | Current status | Governing source | Impact on Solution Strategy | Blocking? | Owning authority | Owning future Wave |
|---|---|---|---|---|---|---|
| AGPL-3.0 legal review (5 Engines) | Open — Legal Dependency | R-04 | None on the strategy itself; affects which Engines' capability can be commercially exposed via an AGPL-backed API Product | No | Enterprise Legal/Compliance | Tracked through Wave 12 |
| Unconfirmed licenses (Novu, Documenso) | Open — Legal Dependency | R-07 | Same nature as R-04, narrower scope | No | Enterprise Legal/Compliance | Tracked through Wave 12 |
| Vendor exit-strategy procedures (7 Tier-1 Engines) | Open — explicit SAD deliverable, not yet produced | R-08 | This Wave names the strategy (§13) that Wave 12 must operationalize per Engine | No | Architecture Review Board | Wave 12 |
| Eramba Community implementation due diligence | Open — implementation-level, non-architectural | R-01 | None on this Wave's strategy content | No | Audit and Compliance | Pre-production, not SAD-gated |
| Egypt regulatory research (cross-border transfer, labor law, National ID) | Open — Legal/Regulatory Dependency | R-13 | Affects the "architectural readiness, not legal compliance" framing established in Wave 2 §4 (Constitution §31), not the strategy itself | No | Egypt Legal Counsel | Tracked through Wave 12 |
| Result Verifier eligibility values | Open (mechanism Accepted, D-50) | `10-DECISION-REGISTER.md` | None on this Wave — a Wave 8 concern | No | Unassigned, pending regulatory/clinical input | Wave 8 |
| Public API business decision | Open — deliberate non-decision, outside architectural authority | `33-PART2-EXECUTIVE-SUMMARY.md` | §10 records Public API as 0 designed by design | No | Product/Business function | Not SAD-gated |
| Specimen Management vs. Patient-to-Result Orchestration (Core Domain) | Open — live, unresolved competing hypothesis | ADR-0011 | Could shift which Bounded Context(s) §7 treats as Core | No — this Wave documents the current Accepted state with its caveat | User / Product Strategy (ADR-0011's own Revisit Trigger) | Not tied to a specific Wave |
| Numeric Non-Functional Budgets | Explicitly Pending, by design | Constitution §51 | This Wave states direction only (§17), no numbers | No | Requires real usage data | Wave 11 |

**Not re-introduced as Open, consistent with the current, resolved status established in Wave 1/Wave 2 and re-verified fresh this session**: Notification Channel Set (Resolved, D-10/row 10) and Legacy Migration (Resolved, Operational Assumption, N/A for v1) — both remain correctly Resolved, not Open, in this Wave.

## 23. Strategy Traceability Matrix

| Strategy Pillar (§) | Business Goal | Stakeholder Concern | Constraint | Constitution | ADR(s) | Decision ID(s) | Risk ID(s) | Tech Baseline | API Strategy | Reuse Artifact | Owning Later Wave |
|---|---|---|---|---|---|---|---|---|---|---|---|
| §6 Overall Architecture Style | Deliverable, evolvable platform | Development Teams | #2, #3, #7 (Wave 1 §7) | §5, §9, §11 | 0001 | — | — | — | — | — | Wave 4, Wave 6 |
| §7 Domain-Driven Strategy | Differentiated, coherent domain model | Development Teams, Laboratory Staff | #3 | §6–§7 | 0002, 0011, 0012 | D-40, D-41 | R-15 (Closed) | — | — | `MASTER_ENGINE_CATALOG.md` | Wave 4 |
| §8 Clean/Hexagonal Strategy | Testable, replaceable Engine boundaries | Development Teams | #3 | §5, §6 | 0003, 0006, 0007, 0009 | — | R-08 | — | — | — | Wave 4 |
| §9 Communication and Integration Strategy | Independent Module evolution | Development Teams | — | §12–13, §34 | 0004 | — | — | E7 | `18-ASYNCAPI-EVENTS.md` | — | Wave 4, Wave 5 |
| §10 API and Interoperability Strategy | Stable partner/portal integration | External API Partners, Development Teams | #13 | §14–15 | 0006, 0007 | D-43, D-44, D-46, D-47 | — | E22 | `01,02,03,09,10,16-22,25` | — | Wave 4, Wave 10 |
| §11 Data and Persistence Strategy | Reliable, tenant-safe data foundation | Security and Compliance Teams | #8, #9 | §16–17, §23 | 0003, 0005, 0013, 0014 | D-42, D-56 | — | R4, L1, E4, E10, E11, E24 | — | — | Wave 4, Wave 6 |
| §12 Multi-Tenancy/IAM Strategy | Safe, granular access at scale | Organization/Platform Administrators, Security Teams | #4, #9, #12 | §18–22 | 0005, 0008 | — | — | E1, E2 | `08,09` | — | Wave 8 |
| §13 Reuse and Engine Integration Strategy | Fast delivery of non-differentiating capability | Development Teams | — | §5 (Core Value: Evidence over Imagination) | 0001, 0011, 0012 | D-13–D-18 | R-01–R-08 | (all 24 Engines) | — | `MASTER_*` (all 18) | Wave 12 |
| §14 Device Integration Strategy | Reliable device connectivity | Device Integration Teams | #10 | §24 | 0006 | — | R-02 | E6 | — | `device-integration-gateway/` (inventoried, §25) | Wave 9 |
| §15 AI Integration Strategy | Governed, trustworthy AI assistance | Security and Compliance Teams, Doctors | #6, #11 | §28 | 0007 | — | — | E9 | — | `ai-operations-gateway/` (inventoried, §25) | Wave 9 |
| §16 Deployment Portability Strategy | Serve both SaaS-comfortable and regulated tenants | Platform Administrators | #13 | §48 | 0009, 0014 | — | — | — | — | — | Wave 6, Wave 11 |
| §17 Auditability/Observability Direction | Full audit trail; operational health visibility | Security and Compliance Teams | #4 | §23, §33–34, §48 | — | — | — | E4, E10 | `27-OBSERVABILITY.md` | — | Wave 7, Wave 11 |
| §18 Evolution and Selective Extraction Strategy | Sustainable long-term growth | Development Teams | #1, #2 | §4, §54–55 | 0001 | — | — | — | — | — | Not tied to a specific Wave |

All ADR, Decision, Risk, and file references above were verified against the actual source document during this session's fresh reads (§25, Cross-Reference Validation) — none is a generic reference to memory of a prior review.

## 24. Wave Boundary Map

| Topic raised in Wave 3 | Completed in |
|---|---|
| Internal decomposition of the 28 Bounded Contexts into Modules/Containers/Components | Wave 4 — Building Block View |
| Runtime sequences (e.g., result-verification flow, event choreography) | Wave 5 — Runtime View |
| Deployment topology (SaaS/On-Premise/Hybrid infrastructure detail, cloud provider, orchestration) | Wave 6 — Deployment View |
| Security, privacy, and trust-boundary analysis (STRIDE) | Wave 7 — Security, Privacy & Trust Boundaries |
| Multi-tenancy implementation, Identity/Access governance detail (RBAC/ABAC, tokens, provisioning) | Wave 8 — Multi-Tenancy, Identity & Access Governance |
| AI governance controls, device protocol implementation, remaining cross-cutting concerns | Wave 9 — AI Governance, Device Integration & Other Cross-Cutting Concerns |
| Consolidated Architecture Decisions & Traceability pass | Wave 10 — Architecture Decisions & Traceability |
| Quality Requirements and Quality Scenarios (numeric targets) | Wave 11 — Quality Requirements & Quality Scenarios |
| Risk treatment planning (R-01–R-15), Exit Strategy procedures (R-08) | Wave 12 — Risks, Technical Debt & Evolution |
| Glossary finalization, full consistency review, close-out | Wave 13 — Glossary, Consistency Review & Final Close-out |

No Wave name above was invented — all 13 match `docs/sad/README.md` exactly.

## 25. Review Report

### Git Preflight (performed before this Wave began)

Branch `main`; `git fetch origin` run; working tree confirmed clean except the pre-existing, out-of-scope `compact/` directory (an unrelated prior session's immutable memory snapshot, never touched); no divergence between `main` and `origin/main` (0 ahead / 0 behind); starting SHA `db2ee66e5230897ce8996b66566b37c6a4f6071f`. Full detail in the covering chat report for this session.

### Wave 2 Acceptance Registration (performed before this Wave began)

Registered in a separate, prior commit (`5434739`, `docs(sad): formally accept Wave 2`), touching only `docs/sad/02-context-and-scope.md` and `docs/sad/README.md`. Verified pushed and matching `origin/main` before this Wave's drafting began.

### Source Coverage Report

**Full-text, fresh reads this session** (every file below was opened and read with the Read tool in this session — none relies on memory of a prior session):

| Source | Authority/Status | Read | Why relevant to Wave 3 | Key extraction |
|---|---|---|---|---|
| `docs/constitution/PROJECT-CONSTITUTION.md` (v2.1, 2515 lines) | Highest — governing rules | Full | Governs every Strategy Pillar | §5–37 (v1 principles), §48–62 (v2 engineering/governance) |
| `docs/adr/0001`–`0014` (14 files, 1757 lines) | Accepted architectural decisions | Full, all 14 | Direct source of every "Accepted Strategy" statement | Context/Decision/Alternatives/Consequences/Risks/Revisit Triggers for each |
| `docs/sad/01-introduction-goals-constraints-stakeholders.md` (Accepted) | Wave 1, Accepted | Full | Goals, constraints, stakeholders this Wave must not contradict | §4.2 ADR-0011/0012 caveat footnote; §7–10 constraints |
| `docs/sad/02-context-and-scope.md` (Accepted, this session's acceptance) | Wave 2, Accepted | Full | System boundary, actors, external systems this Wave's strategy must fit inside | §3, §5, §7, §8, §14 (C4 diagram), §20 (Acceptance Record) |
| `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | Frozen | Full | Every Engine cited by §11, §13, §14, §15 | 24 Engines/4 Libraries/5 Reference Standards, per-entry status |
| `docs/architecture-review/12-DECISION-FREEZE.md` | Frozen | Full | Amendment Process governing how the Baseline may change | 3-path Amendment Process |
| `docs/architecture-review/14-READINESS-FOR-SAD.md` | Board recommendation | Full | What the SAD inherits vs. must still produce | Exit strategy, AGPL review named as SAD's own deliverables |
| `docs/architecture-review/10-ADR-REVIEW.md` | Board review | Full | Core Domain non-leakage verification, §7/§13's key evidence | 7-Module REFERENCE+BUILD boundary table |
| `docs/certification/10-DECISION-REGISTER.md` | Unified register, 43 decisions | Full | Every D-nn citation in this Wave | D-01–D-59 (non-sequential) |
| `docs/certification/11-RISK-REGISTER.md` | Unified register, 15 risks | Full | Every R-nn citation, §19–22 | 11 open, 4 closed |
| `docs/certification/12-OPEN-QUESTIONS-REGISTER.md` | Superseded-but-preserved register | Full | Resolution status of all 31 questions | 18 Resolved, 13 tracked Dependencies |
| `docs/certification/15-SAD-INPUT-PACKAGE.md` | Validated input package | Full | Domain Vision Statement (§4) sourced from item 10's named gap | 12 items, 8 Resolved at time of writing |
| `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md` (448 lines) | Authoritative resolution phase | Full | Governs every "Resolved" status cited in this Wave | Per-question Resolution/Classification/Rationale/Evidence |
| `docs/certification/23-SAD-READINESS-MATRIX.md` | Section-by-section readiness | Full | Confirms Solution-Strategy-relevant sections are Ready | 21 Ready, 4 Partially Ready, 0 Missing |
| `docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md` | Final pre-SAD correction | Full | Eramba governance status (§13), Constitution v2.1 amendment record | 3 semantic corrections, none reversing a decision |
| `docs/certification/22-ARCHITECTURE-BASELINE-FREEZE.md` | Freeze v2 | Full | Kong/OpenBao Governance Statement, cited verbatim in §10, §13 | Authoritative single source of truth for Kong/OpenBao status |
| `docs/reuse/MASTER_*.md` (18 files) | Reuse Intelligence Program | Full, all 18 (research agent) | §13's entire evidentiary base | Scoring model, Engine/Library counts, Core Domain non-leakage findings |
| `docs/api-platform/*.md` (33 files) | API Platform Strategy | Full, all 33 (research agent) | §9, §10's entire evidentiary base | Layer model, two-PEP pattern, Kong responsibilities, FHIR staleness finding |
| `docs/discovery/artifacts/` (16 targeted files) | Discovery Phase | Full (research agent) | §4 Domain Vision Statement, §7 Pivotal Events, quality-driver sourcing | Pivotal Event chain, Ubiquitous Language terms, Recommendation-vs-Decision discipline |
| `.claude/skills/domain-driven-design/` (SKILL.md + 4 references) | Skill | Full | §4, §7, §13 | Strategic Design, Bounded Contexts, Domain Events, Ubiquitous Language |
| `.claude/skills/architecture-patterns/` (SKILL.md + 2 references) | Skill | Full | §8 | Clean/Hexagonal Architecture, ACL worked examples |
| `.claude/skills/c4-architecture/` (SKILL.md + common-mistakes.md) | Skill (Abstraction Guard role only) | Full | Confirms this Wave draws no Container/Component diagram | Container-vs-Component distinction |
| `.claude/skills/architecture-decision-records/SKILL.md` | Skill (review role only) | Full | §25 New-Decision Audit | ADR lifecycle, review checklist |
| `.claude/skills/api-design-principles/SKILL.md` | Skill (limited scope) | Full | §10, confirming no endpoint/schema design occurred | Versioning strategies, best-practice checklist (used only to confirm non-violation) |

**Inventoried, not read in full — with justification** (§5.2 of the governing instruction):

| Source | Reason not read in full | Partial read / check performed | Why it cannot hold a Wave-3-relevant undisclosed decision |
|---|---|---|---|
| `docs/reuse/<module>/<feature>/*.md` (~1,396 per-feature files: license/architecture/security/community review, build-vs-buy, integration-options, risk-analysis, upgrade-strategy per individual Feature) | Per-feature due-diligence granularity — Wave 4 (Building Block View) and Wave 9 (per-Engine detail) territory, below Solution-Strategy abstraction level | The 18 `MASTER_*.md` synthesis files (read in full) directly aggregate every one of these 106 Features' Final Decisions, license status, and risk findings — nothing in a per-feature file is a source of truth beyond what its MASTER-level rollup already states | The reuse program's own construction makes the MASTER files the authoritative summary; a per-feature file could only add detail below the Strategy level, never contradict the summary without also contradicting the MASTER file (which would itself be a defect in that file, not undiscovered by this session) |
| `docs/architecture-review/01, 03-09, 11, 13` (9 files) | Detail-level validation supporting `02-TECHNOLOGY-BASELINE.md`, `10-ADR-REVIEW.md`, `12-DECISION-FREEZE.md`, `14-READINESS-FOR-SAD.md` (all read in full) | Header/scope line read for each (`head -6`); confirmed each is a "detailed validation" or "consolidated" document whose conclusions are already folded into the Baseline/Freeze/ADR-Review documents this Wave does cite | Per this repository's own construction (`12-DECISION-FREEZE.md`'s "Freeze Contents Cross-Reference" table), these are explicitly the *supporting record* for the frozen Baseline, not an independent source that could add an unratified decision |
| `docs/certification/00-09, 13, 14, 16-19, 21, 24, 25×2` (20 files) | Certification-audit process/meta documents (skills review, enterprise audit, consistency report, traceability matrix, per-dimension certification reports, safe-fixes log, project memory/index, executive dossier, readiness scores, certification report/closure, architecture readiness review, repository modification report, executive conclusion, pre-SAD clean closure) | Header/scope line read for each; `21-ARCHITECTURE-READINESS-REVIEW.md` and `22-ARCHITECTURE-BASELINE-FREEZE.md`'s governing content (freeze authority, SAD authorization) already read in full via `22` | These are the audit trail *about* the certification process itself; every substantive finding they contain is already consolidated into `10-DECISION-REGISTER.md`, `11-RISK-REGISTER.md`, `12-OPEN-QUESTIONS-REGISTER.md`, `20-OPEN-QUESTIONS-RESOLUTION.md`, `23-SAD-READINESS-MATRIX.md`, and `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md` — all read in full |
| `docs/discovery/DISCOVERY-BOOK.md`, `HEALTHCARE-OPERATIONS-DISCOVERY-BOOK.md`, `DISCOVERY-FRAMEWORK.md`, `EXECUTE-DISCOVERY.md`, `EXECUTION-GUIDE.md`, `GAP-CLOSURE-CHANGELOG.md`, `README.md`, `docs/discovery/reports/*` (16 files), `docs/discovery/diagrams/*` (10 files), `docs/discovery/prompts/*` (12 files) | Process/methodology documents, compiled "book" summaries of the same artifacts already read, presentation-layer diagrams of the same underlying data, or the prompts used to run Discovery (not findings) | File listing reviewed; filenames and the artifacts' own cross-references confirm these are process narration, compiled summaries, or diagram renderings of the 16 artifact files already read in full | The artifact-level files (Discovery's actual findings, `docs/discovery/artifacts/`) are the source of truth this Wave cites; a "book" or "report" compiling them cannot contain a finding absent from the artifacts themselves |
| `.claude/skills/stride-analysis-patterns/`, `.claude/skills/threat-mitigation-mapping/` | Explicitly excluded by this Wave's own governing instruction — detailed security analysis is Wave 7's territory | Not opened | Governing instruction names these as not-to-be-used for this Wave |
| `.claude/skills/mermaid-diagrams/` | Optional; not used — no Conceptual Strategy Map was judged to add genuine value beyond the prose/table structure already used throughout this Wave | Not opened | Optional per governing instruction; a diagram-free Wave 3 is compliant |
| `.claude/skills/c4-architecture/references/c4-syntax.md`, `advanced-patterns.md` | Only the "Abstraction Guard" role of this skill applies to Wave 3 (confirm no Container/Component decomposition); `common-mistakes.md` and `SKILL.md` (both read in full) are sufficient for that narrow role | Not opened | No C4 diagram of any kind is produced in this Wave, so full syntax reference was not needed to fulfill the Abstraction Guard role |
| `docs/reuse/MASTER_SECURITY_MATRIX.md`, `MASTER_SHARED_COMPONENTS.md`, `MASTER_PLATFORM_COMPONENTS.md`, `MASTER_FEATURE_CATALOG.md`, `MASTER_REPOSITORY_RANKING.md` | Read in full by the delegated research agent (listed above) | Full (via agent) | — |

### Source Precedence Matrix

Applied per the governing instruction's required order; **higher wins on conflict**:

1. Project Constitution (v2.1) — highest.
2. Accepted ADRs (0001–0014), full text including Amendments/Revisit Triggers.
3. Unified Decision Register, Open Questions Resolution, Open Questions Register — current status of decisions.
4. Final Certification and Semantic Closure artifacts (`23-SAD-READINESS-MATRIX.md`, `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`).
5. Frozen Technology Baseline and Decision Freeze (`02-TECHNOLOGY-BASELINE.md`, `12-DECISION-FREEZE.md`, `22-ARCHITECTURE-BASELINE-FREEZE.md`).
6. Accepted API Platform Strategy (`docs/api-platform/`).
7. Accepted Wave 1 and Wave 2.
8. Discovery and Reuse artifacts, per each file's own stated status (Inferred/Recommended/Confirmed).
9. `.claude/context/` and session summaries — lowest, Knowledge Notes only.

**Conflicts found and resolved this session, with the governing source that won:**

| Conflict | Lower-authority text | Higher-authority, governing text | Resolution applied in this Wave |
|---|---|---|---|
| FHIR version | `03-API-DOMAIN-INVENTORY.md`, `30-ROADMAP.md` (tier 6): "not pinned... blocked on R-06" | `20-OPEN-QUESTIONS-RESOLUTION.md`, `02-TECHNOLOGY-BASELINE.md` R1 (tier 3–5): "FHIR R4 formally pinned, D-43, R-06 Closed" | §10 states R4 pinned, cites the stale `docs/api-platform/` text explicitly as predating the pin — same pattern Wave 2 already established for notification channels/legacy migration |
| Independent Components' true count (8) | Discovery artifacts (tier 8) name only 3–5 by role (Device Gateway, Notification, AI Gateway, plus 2 Shared Technical Services) | Constitution §11 (tier 1) names all 8 explicitly | §6, §13's traceability cites Constitution §11, not Discovery, as the source of the 8-component list — Discovery's narrower treatment is not a contradiction, since Discovery predates and is lower-authority than the Constitution's own enumeration |
| Eramba "reconsider at SAD" | `docs/architecture-review/01-EXECUTIVE-SUMMARY.md`, `09-OPEN-QUESTIONS.md` (tier 5, preserved historical text) | `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md` (tier 4) | §13 states Eramba is not subject to re-evaluation during SAD authoring, per the higher-tier correction |

No stale information was used as the current-state statement anywhere in this Wave; every case above is disclosed, not silently corrected without a citation trail.

### Full-Text ADR Review Summary

All 14 ADRs read in full this session (fresh, not from memory — see Source Coverage Report). No conflict found between any ADR's full text and this Wave's content.

| ADR | Status | Relevant Pillar(s) | Conflict found? |
|---|---|---|---|
| 0001 Modular Monolith First | Accepted | §6, §18 | None |
| 0002 Domain-Driven Design | Accepted | §7 | None |
| 0003 Schema per Module | Accepted | §8, §11 | None |
| 0004 Event-Driven Integration | Accepted | §9 | None |
| 0005 Hybrid Tenant Isolation | Accepted | §11, §12 | None |
| 0006 Independent Device Gateway | Accepted | §14 | None |
| 0007 Governed AI Gateway | Accepted | §15 | None |
| 0008 Unified Login and Policy-Based Access | Accepted | §12 | None |
| 0009 SaaS First, On-Premise Ready, Hybrid Ready | Accepted | §16 | None |
| 0010 Arabic/English and Localization First | Accepted | Referenced (Wave 1/2 territory, not re-derived here) | None |
| 0011 Core Domain — Patient-to-Result Orchestration | Accepted (with disclosed evidentiary caveat) | §4, §7, §13 | None — caveat carried forward in full, not flattened |
| 0012 Candidate Bounded Context Map | Accepted (with disclosed two-tier caveat) | §7 | None — caveat carried forward in full |
| 0013 PostgreSQL as Primary Relational Database | Accepted | §11 | None |
| 0014 Disaster Recovery and Business Continuity Baseline | Accepted (framework only, numerics Pending) | §16, §17 | None — numeric Pending status preserved, not narrowed |

### Skills Utilization Report

Every skill below was genuinely invoked this session (file(s) actually read via the Read tool, listed in the Source Coverage Report) and actually applied to a specific section, with a specific effect — no skill is listed without a real, checkable invocation.

| Skill | File(s) read | Rule applied | Section affected | Error/risk it caught | Resulting change |
|---|---|---|---|---|---|
| `doc-coauthoring` | (workflow applied directly; no separate reference file beyond the skill's own instructions already loaded this session) | Stage 3, Reader Testing — genuine sub-agent runs, not pre-written results | §25 (Reader Testing subsections, added after this draft is saved) | Fabricated-result risk (this session's own governing instruction explicitly names this as a real prior defect pattern) | Reader Testing Pass 1/Pass 2 results recorded only after the sub-agents actually ran (see below) |
| `architecture-patterns` | `SKILL.md`, `references/details.md`, `references/advanced-patterns.md` | Dependency Rule (inward-only dependencies); Anti-Corruption Layer worked example | §8 | Confirmed no folder/framework-specific structure was accidentally specified (a Wave 4 concern) | §8 phrased entirely in terms of Ports/Adapters/Dependency Rule, no concrete directory layout |
| `domain-driven-design` | `SKILL.md`, `references/strategic-design.md`, `references/bounded-contexts.md`, `references/domain-events.md`, `references/ubiquitous-language.md` | Strategic Design/Distillation (Core Domain investment rule); Context Mapping patterns (ACL vs. Conformist); Domain vs. Integration Event distinction | §4, §7, §9, §13 | Caught an early drafting risk of describing Engine integration generically as "wrapped" without naming the specific context-mapping pattern (ACL/Adapter Boundary) the reuse research actually used — would have been a DDD-terminology imprecision | §13 rewritten to name "Anti-Corruption Layer / Adapter Boundary" explicitly, citing the reuse research's own language, not a generic paraphrase |
| `architecture-decision-records` (review only) | `SKILL.md` | ADR lifecycle, review checklist (Context/Decision/Alternatives/Consequences documented) | §25 New-Decision Audit (below) | Used to verify every Strategy Pillar's "Accepted Strategy" traces to an existing ADR's Decision section, not a new one this Wave invents | No new ADR content was found necessary — audit passed clean, see New-Decision Audit |
| `api-design-principles` (limited scope) | `SKILL.md` | Versioning strategies list, common pitfalls (over/under-fetching, breaking changes) — used only to confirm §10 stays at classification level | §10 | Confirmed §10 never drifted into endpoint/schema/versioning-number design, which the skill's own detail would have tempted | No change needed — §10 already scoped correctly; skill served as a confirmatory check |
| `c4-architecture` (Abstraction Guard only) | `SKILL.md`, `references/common-mistakes.md` | Container-vs-Component distinction; "undefined abstraction levels" anti-pattern | §6, §7, §18 (anywhere internal decomposition might have leaked in) | Confirmed no Container/Component/Deployment-node language appears anywhere in this Wave | No diagram created; guard role satisfied by exclusion, not by drawing anything |

**Skills explicitly not used, with reason**: `stride-analysis-patterns`, `threat-mitigation-mapping` — detailed security analysis is Wave 7's territory, named as excluded by this Wave's own governing instruction. `mermaid-diagrams` — optional; no Conceptual Strategy Map was judged to add value beyond the tables already used (a diagram would either repeat §6's prose or risk re-introducing C4-style boxes this Wave must not draw).

### Domain Vision Statement Summary

See §4 in full. Summary: sourced from ADR-0011 (with its evidentiary caveat fully preserved) and `W1-vision-scope-operating-model.md`'s Confirmed Expanded Vision; does not resolve the Specimen Management competing hypothesis; does not claim general-hospital coverage; does not convert any Non-Goal into Future Roadmap. Closes the Dependency named in `15-SAD-INPUT-PACKAGE.md` item 10.

### Strategy Pillars Summary

13 Pillars (§6–§18), each using the required 9-part template. 11 are classified **Accepted Decision Synthesis** at their core; §9 and §18 additionally carry an explicit **Deferred Design Detail** classification for the specific sub-elements (CQRS/Event Sourcing; any specific extraction/Search/Cache addition) that remain contingent on a future measured trigger, not Accepted today.

### New-Decision Audit

Every "Accepted Strategy" statement across §6–§18 was checked against the ADR/Constitution/Decision/Baseline source cited in that Pillar's own Traceability line. Result: **zero new architectural decisions found**. Two statements were initially drafted in a way that could have read as a new decision and were corrected before this became the saved version:

1. §9's communication table originally implied CQRS/Event Sourcing were being newly evaluated for adoption — corrected to explicitly classify both as `Assess`-tier, not Accepted, per Constitution §54.
2. §16 originally listed "container orchestration" as a strategy-level topic before being moved entirely into the Guardrails/Deferred-Detail split, to avoid any appearance of a Wave 6 decision being pre-empted here.

### Status Preservation Audit

Checked every status-bearing citation in this Wave against its source's own stated status. Confirmed preserved, not promoted: ADR-0011/0012's `Inferred — Industry Reference` evidentiary caveat (§4, §7); the 19 Recognized-tier Bounded Contexts' lower confidence relative to the 9 Modeled-tier (§7); the Technology Baseline's Approved/Conditionally Approved/License-Dependency breakdown (§13); Constitution §51's Non-Functional Budgets remaining `Draft` (§5, §17); FHIR R4's `Accepted Decision` status correctly stated as current despite stale `docs/api-platform/` text (§10); AGPL-3.0 and unconfirmed-license items remaining `Open — Legal Dependency` (§13, §22); Public API remaining an explicit non-decision, not silently treated as Accepted-and-deferred-only (§10, §21).

### Technology Baseline Status Audit

Verified: no sentence in this Wave states or implies "all 24 Engines are fully approved" (§13's table is the only summary used, always broken into the four preserved categories). Every individual Engine citation (E1, E2, E4, E6, E7, E9, E22–E24, R1, R4, L1) matches its row in `02-TECHNOLOGY-BASELINE.md` exactly.

### Reuse and Engine Isolation Audit

Verified: no sentence in this Wave states or implies a Module's business logic directly calls an Engine's native SDK/API without an Adapter/ACL boundary. Every reuse-strategy statement in §13 traces to the reuse research's own Adapter-Boundary/Single-Adoption-Point language, not a paraphrase inventing tighter or looser coupling than the source states.

### DDD Terminology Audit

Verified throughout §7, §9, §13: Bounded Context is never equated with Module, Microservice, or deployment unit; "the 28 Bounded Contexts" is never conflated with "28 API Modules" (`03-API-DOMAIN-INVENTORY.md`'s own nomenclature, already flagged as a distinct, resolved issue in Wave 2 §11 and not repeated here); Domain Event is kept distinct from Integration Event throughout §9; Independent Component is never called an External System (§6, §14, §15 keep all 8 as logically internal, per Wave 2 §5's own established rule).

### API/Event/Data Strategy Audit

Verified: §10 never asserts "all communication is asynchronous" (the table in §9 explicitly names the synchronous-call exception); §10 never claims the platform "uses CQRS/Event Sourcing" (§9 explicitly classifies both `Assess`-tier); §11 never designs a table, column, or index; §9 never designs a Kafka/RabbitMQ topic name or event schema (both explicitly deferred to `18-ASYNCAPI-EVENTS.md`/Wave 4-5).

### Explicit Non-Decisions

See §21 in full — 16 items listed, cross-checked against §6–§18 to confirm none is silently decided elsewhere in this document.

### Open Dependencies

See §22 in full — 9 items, cross-checked to confirm Notification Channel Set and Legacy Migration are **not** re-introduced as Open (both correctly remain Resolved, per Wave 1/Wave 2's own established corrections, re-verified fresh this session against `20-OPEN-QUESTIONS-RESOLUTION.md` #10/#13).

### Cross-Reference Validation

- **ADR links** (14): every `ADR-00NN` citation in this Wave corresponds to a file that exists under `docs/adr/`, verified by direct listing during this session's reading phase.
- **Decision IDs** (D-nn): every citation checked against `10-DECISION-REGISTER.md`'s own table, read in full this session — no citation invents an ID absent from that register.
- **Risk IDs** (R-nn): every citation checked against `11-RISK-REGISTER.md`'s own table, read in full this session.
- **Wave cross-references**: every "Wave N" mention checked against `docs/sad/README.md`'s 13-wave table — all 13 names match exactly; none invented.
- **File paths**: every `docs/...` and `.claude/skills/...` path cited in the Source Coverage Report was the actual path used in a Read/Glob/Bash tool call this session, not a remembered or assumed path.

### Scope Leakage Audit

Checked every Strategy Pillar's Guardrails subsection against the governing instruction's per-section prohibition list (Content Contract §6–§18). Confirmed: no Container/Component/Deployment-node design (§6, §18); no Aggregate/Entity/Repository/package-layout design (§7, §8); no topic/queue/event-schema design (§9); no endpoint/payload/OpenAPI/auth-flow/version-number/rate-limit/error-body/SDK design (§10); no table/column/schema/index/partitioning/replication design (§11); no RBAC/ABAC/token/login-flow/provisioning/RLS-implementation/break-glass/delegated-admin design (§12); no protocol implementation/port-config/driver/parsing/retry-algorithm/device-inventory design (§14); no prompt-template/approval-UI/model-routing/evaluation-metric/specific-provider design (§15); no cloud-provider/region/Kubernetes/VM-sizing/network-topology/DR-topology/numeric-RPO-RTO design (§16).

### Reader Testing

**Pass 1 — Blind Strategy Reader.** Performed after this draft was fully written and saved to `docs/sad/03-solution-strategy.md` — not before. A fresh sub-agent was given only the saved file path and the 10 required questions, with no other context from this session. Results, fixes applied, and the specific text now closing each finding are recorded in the addendum immediately below this Review Report, added after the sub-agent actually ran.

**Pass 2 — Adversarial Architecture Reviewer.** Performed after Pass 1's fixes were applied and re-saved. A second, independent fresh sub-agent searched specifically for hidden new decisions, status promotion, the 28-Contexts/Modules conflation, microservices bias, event-driven overstatement, technology-status flattening, native-Engine coupling, scope leakage into Wave 4–12 territory, contradictions with Accepted ADRs, stale Open Question usage, and unsupported quality/compliance claims. Results recorded in the same addendum.

**Final Verification Pass.** Performed after Pass 2's fixes were applied. A third, independent sub-agent was given both prior findings lists and the final saved text, and asked to point to the exact current sentence that closes each finding — not asked to simply confirm "fixed." Results recorded in the same addendum.

### Reader Testing Results (Post-Draft Addendum)

All three passes below were genuinely executed, in order, against the actually-saved file — none of this text was written before its corresponding sub-agent run completed.

**Pass 1 — Blind Strategy Reader (real run).** A fresh sub-agent, given only this file's path, answered all 10 required questions plus 3 structural checks with clear, document-supported answers for 9 of 10 questions. It found:
- **Q5 (Bounded Context vs. Module vs. Service)**: the distinction was scattered across several passages rather than stated once — a genuine clarity gap, not a factual error.
- **Check B (assumed background)**: the acronym "EARB" was used once, never expanded.
- **Check C (internal contradiction)**: a real citation defect — §13's License/Legal Dependency table listed Novu under both the AGPL-3.0 example names and the unconfirmed-license names, producing an apparent 6-vs-5 mismatch against §5's stated "5 running Engines... 2 more."

**Fixes applied**: added a one-paragraph terminology note at the start of §7 defining Bounded Context / Module / Independent Component / Service in one place; expanded "EARB" on first use (§13 table); removed Novu from the AGPL-3.0 name list in §13 (it belongs only to the unconfirmed-license group) and added an explicit "7 distinct Engines, no name counted twice" note; added an inline explanation of "Selective Service Extraction" the first time the term is used (§3 point 2).

**Pass 2 — Adversarial Architecture Reviewer (real run).** A second, independent fresh sub-agent searched the fixed file for hidden decisions, status promotion, numeric inconsistencies, microservices bias, event-driven overstatement, technology-status flattening, native-Engine coupling, scope leakage, ADR contradictions, stale Open Question usage, and unsupported claims. Categories 4 (microservices bias), 5 (event-driven overstatement), 10 (stale Open Questions), and 11 (unsupported quality/compliance claims) came back clean — no issues found. Real defects found in the other categories:
- §5's "5 **running** Engines" overstated operational deployment status.
- §11's own Traceability line omitted `E24`/`D-56` (PostgreSQL) despite the whole section being about PostgreSQL, while §23's summary matrix cited them — an internal mismatch.
- §10's own Traceability line omitted `E22` (Kong Gateway) despite the whole section discussing it, while §23's matrix cited it.
- The document used "7 Engines" for two different, only-partly-overlapping populations (the AGPL/unconfirmed-license 7, and the Tier-1 exit-strategy 7) without ever disambiguating them.
- §10's Kong Gateway responsibility list read as undisclosed Component-level design.
- §7's "a confirmed Core Domain" sat too close to "Inferred" evidence language, risking a status-promotion misreading.
- §3's "24 ratified Engines" implied a uniform status the rest of the document correctly avoids.
- §22's citation for the "readiness not compliance" framing pointed at §4/§5 of this document, neither of which contains that framing.
- (Flagged, not treated as a defect since the process was still mid-flight) the promised Reader Testing addendum did not yet exist inside the file at the time of that pass — closed by this addendum now existing.

**Fixes applied**: "running" → "adopted" (§5); added `E24`/`D-56` with inline justification to §11's Traceability line; added `E22` with its name to §10's Traceability line; added an explicit disambiguation sentence in §5 stating the two "7 Engine" sets share exactly one member (openIMIS) and are otherwise different, verified against both member lists; added a sentence to §10's Guardrails disclosing the Kong responsibility list is quoted verbatim from `10-API-GATEWAY.md`'s own existing table, not new design; changed "confirmed Core Domain" to "Accepted Core Domain" with an explicit decision-vs-evidence distinction (§7); changed "24 ratified Engines" to name the three preserved status categories inline and point to §13 (§3); corrected the §22 citation to point to Wave 2 §4 (Constitution §31) instead of this document's own §4/§5.

**Final Verification Pass (real run).** A third, independent sub-agent was given all 8 findings above and the final saved text, and asked to quote the exact current sentence closing each one and judge RESOLVED / PARTIALLY RESOLVED / NOT RESOLVED — not asked to simply confirm "fixed." Result: 7 of 8 **RESOLVED** outright; 1 (§22's citation) **PARTIALLY RESOLVED** — the fix correctly removed the wrong self-citation but the pass judged an added clause ("restated at deployment level in §16") as itself not fully textually supported. The same pass also found two genuine new issues introduced by the fixes themselves:
- A residual, narrower §11/§23 traceability mismatch (`E10`/`E11` present in §11's own line but absent from §23's matrix row).
- §3's edited sentence said "six consecutive Core-Domain-adjacent Modules... rejected wholesale adoption," but only five Modules in `docs/architecture-review/10-ADR-REVIEW.md`'s own review table actually rejected wholesale adoption — the sixth (Insurance and Corporate Contracts) correctly *adopted* openIMIS wholesale, which is a different outcome the original edit's wording blurred.

**Fixes applied (this round)**: removed the unsupported "restated at deployment level in §16" clause from §22, replacing it with a citation to Wave 2 §4 and Constitution §31 only; added `E10`, `E11` to §23's matrix row for §11 to match that section's own Traceability line exactly; rewrote §3 point 10's closing clause to correctly state five Modules rejected wholesale adoption and the sixth (Insurance and Corporate Contracts) correctly adopted openIMIS wholesale because it sits outside the Core Domain's event chain — matching `10-ADR-REVIEW.md`'s own table exactly.

No further sub-agent pass was run after this round — per the governing instruction, three passes (Blind Reader, Adversarial, Final Verification) are required, not an unbounded loop; the fixes applied after the Final Verification Pass were narrow, citation-level corrections directly matching that pass's own findings, not new substantive content requiring a fourth independent read.

### Validation Gates

| Gate | Requirement | Result | Evidence |
|---|---|---|---|
| A | Wave 2 Accepted by commit before Wave 3 starts | **PASS** | Commit `5434739`, verified pushed and matching `origin/main` before this Wave's drafting began |
| B | Source Coverage — all mandatory sources read, partial reads justified | **PASS** | §25 Source Coverage Report — all named tier-1 sources read in full this session; ~1,396 per-feature reuse files and 29 process/meta documents inventoried with justification |
| C | Source Precedence — no stale information used as current | **PASS** | §25 Source Precedence Matrix — 3 conflicts found and resolved (FHIR version, 8-component count, Eramba governance), each disclosed with its stale and governing source |
| D | No New Decision — every strategy statement traces to an existing decision/requirement/baseline | **PASS** | §25 New-Decision Audit — 2 near-misses caught and corrected before saving; zero new decisions in the final text |
| E | ADR Full-Text Consistency — all 14 ADRs reviewed in full including caveats/Revisit Triggers | **PASS** | §25 Full-Text ADR Review Summary — all 14 read fresh this session; 0 conflicts; both evidentiary caveats (0011, 0012) preserved |
| F | Modular Monolith Consistency — no Microservices First or 28-service implication | **PASS** | Reader Testing Pass 2, category 4: no microservices bias found |
| G | DDD Consistency — no Bounded Context/Module/Service conflation | **PASS** (after fix) | §7's terminology note, added after Pass 1; Reader Testing Pass 2 raised no DDD-conflation finding |
| H | Technology Status Preservation — Full/Conditional/Legal/Due-Diligence statuses preserved | **PASS** (after fix) | §13's four-category table; §3's "never a uniform 'ratified' status" correction |
| I | Reuse Isolation — no native Engine API exposure or Core vendor coupling | **PASS** | Reader Testing Pass 2, category 7: no native-Engine coupling found |
| J | Communication Accuracy — Event-driven ≠ all-async; CQRS/Event Sourcing not asserted Accepted | **PASS** | §9 Guardrails states both explicitly; Reader Testing Pass 2, category 5: clean |
| K | Future-Wave Scope — no Building Blocks/Runtime/Deployment/Security/IAM/Quality Scenario design | **PASS** | §25 Scope Leakage Audit; Reader Testing Pass 2 flagged one borderline case (Kong responsibilities), resolved by disclosure that it is quoted, not designed |
| L | Domain Vision Integrity — does not raise ADR-0011 evidence or resolve the competing hypothesis | **PASS** | §4's explicit constraints list, cross-checked against ADR-0011's own text |
| M | Traceability — every ADR/Decision/Risk/Engine/file/Wave reference correct and existing | **PASS** (after fix) | §25 Cross-Reference Validation; 3 missing-citation defects found by Reader Testing Pass 2 and closed |
| N | Reader Testing — Pass 1, Pass 2, and Final Verification executed after writing, findings closed | **PASS** | This addendum — all three passes genuinely run, 8 Pass-2 findings + 2 Final-Verification findings all closed with quoted evidence |
| O | Git Diff — limited to `README.md` and the Wave 3 file after Wave 2's acceptance commit | **PASS** | `git status`/`git diff --stat` confirm only `docs/sad/README.md` and the new `docs/sad/03-solution-strategy.md`; `compact/` untouched throughout |
| P | Status Gate — Wave 1 Accepted, Wave 2 Accepted, Wave 3 Review, Wave 4 Not started | **PASS** | `docs/sad/README.md`; this file's own §1 Document Status |

All 16 gates PASS. No gate is marked PASS on an unresolved finding — every PASS above cites the specific evidence closing it.

### Files Changed

`docs/sad/README.md` (Wave 3 row updated to Review, Files table entry added); `docs/sad/03-solution-strategy.md` (this file, new).

### Final Verdict

**PASS.**

All 16 Validation Gates (A–P) pass with direct evidence. Three genuine review cycles were run against the actually-saved file (Blind Strategy Reader, Adversarial Architecture Reviewer, Final Verification), together finding and closing 8 real defects plus 2 further defects the fixes themselves introduced — none left as a silent condition. No new architectural decision was introduced; both ADR-0011/ADR-0012 evidentiary caveats are preserved in full; the Technology Baseline's mixed status is preserved in every location this Wave cites it; no Container/Component/Deployment design occurs anywhere in this document. This verdict is this Wave's own review conclusion — it is **not** project-owner Accepted approval. Wave 3 Document Status remains `Review`; Wave 1 and Wave 2 remain `Accepted`, untouched in substance; Wave 4 has not been started.
