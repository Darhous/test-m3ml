# Context Map (Discovery, Phase 06)

**Status: Draft — Assumption-Driven Autonomous Run.** Standalone summary of
the Context Map; full rationale per relationship is in
`06-bounded-contexts.md`. See `docs/discovery/diagrams/06-context-map.md`
for the visual diagram.

## Contexts (8)

Order Management · Specimen Management · Test Processing and Result
Verification (**Core**) · Notification and Communication · Billing and
Claims · Device and Equipment Integration · Core Platform — Identity and
Access · Core Platform — Organization and Branch.

## Relationships (11 edges, all named)

1. Order Management → Core Platform (Identity and Access): Open Host
   Service + Published Language
2. Order Management → Core Platform (Organization and Branch): Open Host
   Service + Published Language
3. Specimen Management → Order Management: Customer/Supplier
4. Specimen Management → Core Platform (both): Open Host Service +
   Published Language
5. Test Processing and Result Verification → Specimen Management:
   Customer/Supplier
6. Test Processing and Result Verification → Order Management:
   Customer/Supplier
7. Test Processing and Result Verification → Core Platform (both): Open
   Host Service + Published Language
8. Test Processing and Result Verification ↔ Device and Equipment
   Integration: Anti-Corruption Layer (consumer side) / Open Host Service
   (provider side), event-based
9. Notification and Communication ← {Specimen Management, Test Processing
   and Result Verification, Billing and Claims}: Open Host Service +
   Published Language, event-based
10. Billing and Claims → Test Processing and Result Verification: Open Host
    Service + Published Language, event-based
11. Billing and Claims → Order Management: Customer/Supplier

**Zero unlabeled relationships** — Constitution Section 7's Context Map
Completeness requirement satisfied (Constitution Section 49 Fitness
Function: DDD Boundaries).

**Zero Shared Kernels adopted** — one was explicitly considered
(Organization/Branch reference data) and rejected in favor of Open Host
Service; see `06-bounded-contexts.md` for the reasoning. No ADR is
triggered.
