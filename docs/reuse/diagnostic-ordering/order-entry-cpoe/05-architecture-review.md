# Architecture Review — Order Entry / CPOE

The platform's own Order Aggregate is modeled as a FHIR `ServiceRequest`,
with a `Task` construct tracking its orchestration state through
Specimen Operations (Module 13) and Laboratory Execution (Module 14) —
directly reusing the proven OpenHIE/OpenELIS pattern's *shape* without
adopting OpenELIS itself. This keeps the deepest modeling investment in
this platform's own Core Domain (ADR-0011 Amended) while still reusing a
battle-tested integration architecture, not inventing one from scratch.
