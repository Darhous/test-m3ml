# Global Search Log — Order Entry / CPOE

**Query:** `open source LIS lab order entry SENAITE vs OpenELIS Global
vs Bahmni 2026 CPOE ServiceRequest`

**Finding:** **OpenELIS Global** uses a proven FHIR-standard pattern
(OpenHIE-aligned): the ordering system creates a `ServiceRequest` +
`Task` (status "requested"), the LIS receives the `Task` (referencing
the ServiceRequest via `Task.basedOn`) and creates its internal order —
a real, production-proven order-orchestration architecture, not a
theoretical one. **Bahmni** (OpenMRS-based) implements the ordering side
of this exact pattern in production. **SENAITE** is noted as more
full-service (covers microbiology, where OpenELIS has gaps) — directly
relevant to Module 14 (Laboratory Execution), not this Feature.

**Scoping note (consistent with Modules 9-11):** OpenELIS/Bahmni are
themselves full clinical systems: adopting either wholesale for order
entry specifically would still risk Core-Domain encroachment. Their
**FHIR ServiceRequest + Task pattern**, however, is a proven, reusable
*architecture*, not a whole-system dependency — the same distinction
this program has applied consistently.
