# Final Decision — Consent Management

## Decision: **REFERENCE (FHIR `Consent` data model) + BUILD (enforcement, reusing OPA)**

No standalone Engine exists for this Feature's actual scope (clinical
consent), so no product is force-fit. FHIR gives a proven, standards-body
data-model Reference; enforcement reuses the already-selected OPA
integration rather than introducing a new rules engine — a direct
Cross-Feature Dependency win.
