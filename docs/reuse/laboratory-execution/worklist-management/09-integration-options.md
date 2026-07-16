Not applicable as a product integration (no Engine adopted). The
platform-owned Worklist Aggregate integrates internally with
`specimen-accessioning` (Module 13, upstream) and `order-entry-cpoe`
(Module 12, upstream) via the shared FHIR `ServiceRequest`/`Task` state
pattern, and feeds `analyzer-middleware-integration` (below) and Module
15 (Result Verification, downstream).
