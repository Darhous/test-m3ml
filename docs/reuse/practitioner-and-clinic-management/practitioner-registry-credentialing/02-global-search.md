# Global Search Log — Practitioner Registry / Credentialing

No new search round — reuses Module 9's finding (HL7 FHIR data-model
Reference over whole-system EMR adoption). FHIR's `Practitioner` and
`PractitionerRole` resources (identity, qualifications, roles) are the
direct analog to the already-adopted `Patient` resource pattern. No
dedicated open-source "credentialing engine" of comparable maturity to
OpenMRS/HAPI FHIR was identified as a distinct category — credentialing
tracking (license expiry, renewal) is a workflow layer on top of the
FHIR-shaped identity data, not a separate product category.
