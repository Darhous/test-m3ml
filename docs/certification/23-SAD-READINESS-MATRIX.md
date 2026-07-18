# SAD Readiness Matrix

All 25 sections named in this phase's mandate. **Readiness** here means
"sufficient decided inputs exist to author this section," not "the
section is pre-written" — drafting the SAD is the next phase's own
work.

| # | SAD Section | Status | Justification |
|---|---|---|---|
| 1 | Executive Summary | **Ready** | Vision, mission, market (Egypt-first), platform positioning fully decided (`.claude/context/vision.md`, Constitution §1-4). |
| 2 | Architectural Drivers | **Ready** | Constitution §5 Architecture Principles, 14 Accepted ADRs, Discovery's business/value-stream evidence. |
| 3 | Quality Attributes | **Partially Ready** | Category framework exists (Constitution §48 Engineering Principles, §49 Fitness Functions), but §51 Non-Functional Budgets are explicitly Draft with no numeric targets (correctly not invented, pending Open Question #4 real usage data). |
| 4 | Constraints | **Ready** | `.claude/context/constraints.md` (14 Confirmed constraints), Constitution sections. |
| 5 | Context Diagram | **Ready** | All actors (39-Persona catalog), external systems (24 ratified Engines), and boundaries needed to draw one are fully documented; no C4 diagram has been drawn yet, but that is SAD-original drafting work, not a blocked input. |
| 6 | Bounded Contexts | **Ready** | ADR-0012 Accepted — 28 contexts (9 Modeled, 19 Recognized), full Context Map in `docs/discovery/artifacts/W9-bounded-context-remapping.md`. |
| 7 | Domain Model | **Partially Ready** | Modeled-tier contexts (9) have Evidenced-confidence Aggregate/Value-Object/Domain-Event design (Discovery Phase 05). The 19 Recognized-tier contexts are explicitly lower-depth by ADR-0012's own design — genuine residual tactical-modeling work remains for those, not a blocker but a real gap to close during SAD. |
| 8 | Module Architecture | **Ready** | 28-Module Catalog, ADR-0001 (Modular Monolith), ADR-0003 (Schema per Module), Constitution §8-11. |
| 9 | Runtime Architecture | **Ready** | ADR-0001 sets the style; Constitution §48 (error handling, retry/idempotency/cache/background-job policies) provides the cross-cutting runtime rules the SAD assembles from. |
| 10 | Integration Architecture | **Ready** | ADR-0004 (Event-Driven, RabbitMQ), ADR-0006 (Device Gateway), `docs/api-platform/16-21` (Contract-First, AsyncAPI, Webhooks, Integrations). |
| 11 | API Architecture | **Ready** | 34 `docs/api-platform/` documents — the most thoroughly developed input set in the repository. |
| 12 | Security Architecture | **Ready** | `docs/api-platform/11`, Constitution §29-30, STRIDE applied at 3 layers, OWASP API Top 10 fully mapped. |
| 13 | Identity Architecture | **Ready** | ADR-0008, Keycloak+OPA, `docs/api-platform/08-09`. Minor residual detail (exact Keycloak realm-partitioning shape) is normal SAD-level design, not a blocked dependency. |
| 14 | Device Integration | **Ready** | ADR-0006, Mirth Connect/Apache Camel, Constitution §24, `docs/reuse/device-integration-gateway/`. |
| 15 | AI Architecture | **Ready** | ADR-0007, Portkey Gateway, Constitution §28 (HITL), 7 candidate use cases (Wave 10). |
| 16 | SaaS Architecture | **Ready** | ADR-0009, Kill Bill + OPA entitlement composition, `docs/api-platform/25-26`. |
| 17 | Multi-Tenant Architecture | **Ready** | ADR-0005 + D-42 (PostgreSQL RLS + tenant-ID column, resolved this cycle), `docs/api-platform/14`. |
| 18 | Data Architecture | **Ready** (was Partially Ready) | **Closed 2026-07-18**: Schema-per-Module (ADR-0003), tenant partitioning (D-42), and now the relational engine itself (ADR-0013, PostgreSQL) are all formally decided. The gap this row originally flagged — no document formally naming PostgreSQL — is resolved, not merely deferred. |
| 19 | Event Architecture | **Ready** | ADR-0004, `docs/api-platform/18` (AsyncAPI), RabbitMQ (E7), Domain Event vocabulary in `.claude/context/glossary.md`. |
| 20 | Deployment Architecture | **Partially Ready** | ADR-0009 sets direction (SaaS-First, cloud-replaceable per constraint #13); actual topology (containers, orchestration, specific cloud services) is intentionally undecided, consistent with "replaceable cloud provider" — genuinely SAD-original content, not a blocker. |
| 21 | Observability | **Partially Ready** | `docs/api-platform/27` defines the architecture (metrics/logging/tracing, Superset for dashboards); numeric SLO targets remain deferred pending real usage data (same Open Question #4 dependency as Quality Attributes). |
| 22 | Disaster Recovery | **Ready** (was Missing Inputs) | **Closed 2026-07-18**: ADR-0014 establishes a 4-tier service-criticality classification, backup/recovery/governance principles, and a structured RPO/RTO table. Numeric targets remain honestly labeled Pending Business/Regulatory/Workload Approval — not fabricated — but the SAD now inherits a governed framework rather than a blank section, satisfying this phase's own bar ("the absence of final business-approved numbers must not remain a missing SAD input"). |
| 23 | Technology Mapping | **Ready** | `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` (33 entries: 24 Engines including Kong Gateway, OpenBao, and PostgreSQL as full ratified entries) — the single most complete input in the repository by design. |
| 24 | Risks | **Ready** | `11-RISK-REGISTER.md` — 15 risks, governance metadata (Resolution Gate/Phase/Authority/Evidence) for the 5 highest-severity. |
| 25 | Appendices | **Ready** | Glossary (`.claude/context/glossary.md`), all 14 ADRs, all Master reuse documents — fully available as appendix source material. |

## Summary

**Updated 2026-07-18 (Pre-SAD Baseline Correction).** Rows 18 and 22
moved to Ready this cycle (ADR-0013, ADR-0014).

| Status | Count | Sections |
|---|---|---|
| Ready | 21 | 1, 2, 4, 5, 6, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 22, 23, 24, 25 |
| Partially Ready | 4 | 3, 7, 20, 21 |
| Missing Inputs | 0 | — |

**21 + 4 + 0 = 25.**

## Why the SAD Can Proceed Despite 4 Non-Fully-Ready Sections

None of the 4 represents a blocked architectural decision:

- **3, 21 (Quality Attributes, Observability numerics)**: correctly
  deferred pending real usage data (Open Question #4) — inventing
  numbers now would violate the No-Guessing Rule more than proceeding
  without them.
- **7 (Domain Model depth)**: the 19 Recognized-tier contexts' deeper
  tactical modeling is explicitly SAD/Implementation-phase work per
  ADR-0012's own design — not a blocked dependency, a scheduled one.
- **20 (Deployment Architecture)**: intentionally undecided by design
  (cloud-provider replaceability is itself the architectural position).

**0 sections now have Missing Inputs.** Both gaps identified at the
Architecture Readiness Review (Data Architecture, Disaster Recovery)
are closed by ADR-0013 and ADR-0014 respectively.
