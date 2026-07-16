# Business Capability Map (Discovery, Phase 02)

**Status: Draft — Candidate classification, Assumption-Driven Autonomous
Run.** Every capability below not directly traceable to `vision.md` is
`Inferred — Industry Reference` (standard laboratory information system /
healthcare operations practice), logged in `ASSUMPTION-REGISTER.md`.
Core/Supporting/Generic tags are **Candidate** — final classification is
Playbook 04's job, informed by the Event Storming board (Phase 03).

## Confirmed Framing (from `vision.md`, not invented)

Starting point: Laboratory Management. Long-term: broad healthcare
platform. Central Backend Platform, Unified Login, Portal/Dashboard routing
by Role/Permissions/Data Scope/Organization/Branch. API-First, Event-
Driven, AI-Ready, Integration-Ready. Not a plain CRUD system.

## Capability Map

| Capability | Candidate Class | Basis | Serves Value Stream(s) |
|---|---|---|---|
| Test Catalog Management (define orderable tests, panels, specimen requirements) | Candidate: Supporting | Inferred — Industry Reference | VS1, VS2 |
| Test Ordering (capture an order from a doctor or self-requesting patient) | Candidate: Core | Inferred — Industry Reference | VS1, VS2 |
| Specimen Collection & Chain of Custody (collect, label, track a specimen from patient to lab) | Candidate: Core | Inferred — Industry Reference | VS1, VS2, VS3 |
| Specimen Accessioning (receive and register a specimen at the processing lab) | Candidate: Core | Inferred — Industry Reference | VS1, VS2, VS3 |
| Specimen Rejection & Recollection Handling | Candidate: Core | Inferred — Industry Reference | VS3 |
| Test Processing & Result Capture (analytical phase) | Candidate: Core | Inferred — Industry Reference | VS1, VS2 |
| Result Verification & Release (clinical sign-off before a result is visible to patient/doctor) | Candidate: Core | Inferred — Industry Reference; reinforced by Constitution Section 21/23 Sensitive-Operation framing | VS1, VS2 |
| Clinical Reporting (produce the patient/doctor-facing report artifact) | Candidate: Core | Inferred — Industry Reference | VS1, VS2 |
| Patient & Doctor Communication / Notification | Candidate: Supporting | `vision.md` (Portal routing) + Inferred delivery mechanics | VS1, VS2, VS3 |
| Billing & Invoicing | Candidate: Supporting | Inferred — Industry Reference | VS4 |
| Insurance & Payer Claims | Candidate: Supporting | Inferred — Industry Reference | VS4 |
| Inventory & Reagent Management | Candidate: Supporting | Inferred — Industry Reference | (supports VS1/VS2 indirectly) |
| Device & Equipment Integration | Candidate: Supporting | Constitution Section 24 (Confirmed as a v1 requirement, not invented) | VS1, VS2 |
| Quality Control & Accreditation Compliance | Candidate: Supporting | Inferred — Industry Reference | (cross-cutting) |
| Staff & Operations Management (scheduling, workload) | Candidate: Supporting | Inferred — Industry Reference | (cross-cutting) |
| Organization & Branch Management | Candidate: Supporting | `vision.md` (Organization/Branch routing, Confirmed) | (cross-cutting) |
| Identity & Access (Unified Login, Role/Permission/Policy) | Candidate: Generic | `vision.md` (Confirmed), Constitution Section 20/21 (Accepted) | (cross-cutting, all VS) |
| Audit & Traceability | Candidate: Generic | Constitution Section 23 (Accepted) | (cross-cutting) |
| Notification Delivery Mechanics (channel-agnostic sending) | Candidate: Generic | Inferred — Industry Reference | (cross-cutting) |
| Document/File Storage (reports, device exports, attachments) | Candidate: Generic | Constitution Section 27 (Accepted) | VS1, VS2 |

**Explicitly not yet classified as a capability (Open, per
`open-questions.md` #9):** hospital/clinic-specific capabilities beyond
laboratory scope — `vision.md` confirms the long-term goal is a broad
healthcare platform, but whether hospitals/clinics are in scope for the
first real build is still `Open`. No hospital/clinic-specific capability is
invented here.

## Reader Test Note

A domain expert (e.g., a lab operations manager) reading this table should
recognize every row as "yes, that's what a lab does" — no row names a
system component or technical concept. This map deliberately excludes any
mention of modules, services, or databases (that begins at Phase 06).
