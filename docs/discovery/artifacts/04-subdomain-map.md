# Subdomain Map (Discovery, Phase 04)

**Status: Draft — Candidate classification, Assumption-Driven Autonomous
Run.** Clustered from the 26 events (Phase 03) and 20 capabilities (Phase
02) using the 5 candidate Pivotal Events as seams. Core/Supporting/Generic
classification uses the `domain-driven-design` skill's Strategic Design
test; every Core classification carries a Domain Vision Statement per
Playbook 04 Execution Step 5.

## Candidate Subdomains

| # | Subdomain | Clustered From (events/capabilities) | Classification | Evidence Strength |
|---|---|---|---|---|
| 1 | Order Management | `TestOrdered`; Test Ordering, Test Catalog Management | **Supporting** | Strong (well-evidenced by VS1/VS2) |
| 2 | Specimen Management | `SpecimenCollected`, `HomeVisitRequested/Scheduled`, `CollectorDispatched`, `SpecimenCollectedAtHome`, `SpecimenTransportedToLab`, `SpecimenAccessioned`, `SpecimenQualityChecked`, `SpecimenRejected`, `RecollectionScheduled`; Specimen Collection, Accessioning, Rejection/Recollection capabilities | **Supporting** (see Domain Vision Statement — debated) | Strong |
| 3 | Test Processing & Result Verification | `TestProcessingStarted`, `TestResultCaptured`, `ResultVerified`, `ResultReleased`; Test Processing, Result Verification & Release, Clinical Reporting capabilities | **Core** | Strong |
| 4 | Notification & Communication | `PatientNotified`, `DoctorNotified`, `PatientNotifiedOfRejection`, `DoctorNotifiedOfRejection`, `ReportViewed`; Patient/Doctor Communication capability | **Generic** | Strong |
| 5 | Billing & Claims | `BillableEventIdentified`, `InvoiceGenerated`, `InsuranceEligibilityChecked`, `ClaimSubmitted`, `ClaimAdjudicated`, `PatientBalanceSettled`; Billing, Insurance & Payer Claims capabilities | **Supporting** | Weak (VS4 itself is the shakiest value stream — `open-questions.md` #17) |
| 6 | Identity & Access | (no direct events; cross-cutting per `vision.md` Unified Login) | **Generic** | Strong (already Accepted at Constitution Section 10/20, Core Platform) |
| 7 | Device & Equipment Integration | Lab Analyzer Device, Portable Collection Device (External Systems, Phase 03) | **Supporting** | Medium (already an Independent Component, ADR 0006 — necessary, not itself the differentiator) |
| 8 | Organization & Branch Management | (no direct events; cross-cutting per `vision.md`) | **Generic** | Medium |
| 9 | Inventory & Reagent Management | Phase 02 capability only, no Phase 03 events surfaced it | **Supporting** | **Weak — no Event Storming evidence**, classified from Phase 02 capability alone |
| 10 | Quality Control & Accreditation Compliance | Phase 02 capability only, no Phase 03 events surfaced it | **Supporting** | **Weak — no Event Storming evidence** |
| 11 | Staff & Operations Management | Phase 02 capability only, no Phase 03 events surfaced it | **Supporting** | **Weak — no Event Storming evidence** |

## Domain Vision Statements (Core candidates)

### Test Processing & Result Verification — Core

A laboratory's entire value proposition to a patient and a doctor rests on
one promise: *the result you receive is accurate and someone accountable
verified it before it reached you.* This Subdomain owns that promise end
to end — from raw analytical capture through clinical verification to
release. If a competing lab could process and verify results faster, more
accurately, or more transparently, that would be a direct, patient-visible
competitive differentiator. It is also where the Constitution's Human
accountability principle (Section 4, Core Value) and the platform's
Sensitive-Operation/Audit machinery (Section 21/23) concentrate most
heavily — the deepest modeling investment belongs here.

## Domain Vision Statement (debated candidate — logged for transparency)

### Specimen Management — classified Supporting, with a noted alternative

Specimen Management was classified Supporting because specimen handling,
while operationally critical, is closer to table-stakes competence across
the industry than a differentiator most patients would consciously choose
a lab over. **However**, if this platform's actual competitive strategy
turns out to be convenience/access-led (e.g., home collection reach and
reliability as the primary differentiator, per VS2), Specimen Management —
specifically its Home Collection Logistics slice — could instead be Core.
**This is explicitly flagged as an assumption pending real business
strategy input, not resolved here** (see `ASSUMPTION-REGISTER.md`).

## Proposed Answer to Open Question #14 (Core Domain)

**Proposed (not Accepted):** the Core Domain is **Test Processing & Result
Verification**, on the evidence above. This proposal is carried forward
to Phase 11 (Validation) for consistency-checking and to Phase 12 for
possible ratification via ADR — it is not decided here, per Constitution
Section 39 (ADR-before-Accepted) and `DISCOVERY-FRAMEWORK.md` Section 4
(only Phase 12 may write `Accepted`).

## Divergence from `module-catalog.md`'s 16 Existing Categories

| `module-catalog.md` category | Discovery finding |
|---|---|
| Core Platform Modules | Aligns with Identity & Access + Organization & Branch Management (Generic Subdomains #6, #8) |
| Identity and Access Modules | Aligns directly with Subdomain #6 |
| Organization Modules | Aligns directly with Subdomain #8 |
| Patient Modules | **No distinct Subdomain surfaced** — Patient is an Actor across multiple Subdomains (Order Management, Specimen Management, Notification), not yet evidenced as its own Bounded Context. Flagged as a gap for Phase 06 to resolve, not forced here. |
| Doctor and Clinic Modules | Same as above for Doctor; "Clinic" scope remains Open (`open-questions.md` #9) |
| Laboratory Modules | **Splits into three** Discovery Subdomains: Order Management, Specimen Management, Test Processing & Result Verification — a single "Laboratory" category was too coarse for the evidence found |
| Device Integration Modules | Aligns with Subdomain #7 |
| Workflow Modules | **Not surfaced as its own Subdomain** — workflow/state-transition behavior appears *within* Specimen Management and Test Processing (e.g., specimen QC states, result states), not as a standalone Subdomain. Flagged, not forced. |
| Notification and Communication Modules | Aligns with Subdomain #4 |
| Billing and Finance Modules | Aligns with Subdomain #5 |
| Insurance Modules | **Folded into Billing & Claims** (Subdomain #5) in this pass rather than kept separate — flagged as a divergence for Phase 06 to reconsider once real insurance-model input exists (`open-questions.md` #17) |
| Inventory and Procurement Modules | Aligns with Subdomain #9 (weak evidence) |
| AI and Analytics Modules | Not classified yet — Phase 10's job |
| Integration Modules | Overlaps Subdomain #7 and future Phase 08 findings |
| Security and Compliance Modules | Splits across Subdomain #6 (Generic, Identity/Access) and Subdomain #10 (Supporting, QC/Accreditation — weak evidence) |
| Support and Operations Modules | Aligns with Subdomain #11 (weak evidence) |

## Explicit Caveat on Weak-Evidence Subdomains

Subdomains #9, #10, #11 (Inventory, Quality Control/Accreditation, Staff/
Operations) were classified from Phase 02's Capability Map alone — no
Event Storming evidence exists for them because Phase 02's traced Value
Streams did not touch them. Per Playbook 04's own Common Mistakes warning
("classifying a Subdomain as Core because it is complex rather than
differentiating" — applied here to *any* classification made on thin
evidence), these three classifications should be treated as low-confidence
placeholders, not settled findings.
