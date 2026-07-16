Platform-owned Verification Aggregate wrapping FHIR `DiagnosticReport`'s
status state machine, with each transition gated by an OPA policy
decision (the 8-dimension model: role, data scope, organization/branch,
result criticality, patient consent status, and others per Wave 6) —
same "decision-with-trace" audit shape already established in Module 1's
`authorization-rbac-abac` Reference pattern.
