# Build vs. Buy — Consent Management

No credible Engine/SDK/Library exists for clinical patient-consent
enforcement specifically (the category-mismatch finding in
`02-global-search.md`). The evidence-based, non-fabricated answer is:
**REFERENCE** the FHIR `Consent` data model, **BUILD** the enforcement
logic (reusing the OPA policy-evaluation pattern already selected in
Module 1 rather than a bespoke rules engine). Rejected: forcing Klaro or
a generic cookie-consent tool into this role purely to have a "Buy"
answer — would misrepresent a real capability gap as solved.
