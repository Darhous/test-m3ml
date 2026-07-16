# Upgrade Strategy — Consent Management

FHIR itself versions slowly and deliberately (R4, R5, etc.) with strong
backward-compatibility norms — low churn risk for the data-model
Reference. The platform's own enforcement code follows OPA's upgrade
strategy (Module 1) since it reuses that engine, not a separate one.
