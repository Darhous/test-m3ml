# Reusable Assets — Authorization (RBAC/ABAC)

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| Data Model | Rego input-document schema pattern (attributes → decision) | OPA documentation/examples | Directly informs how to structure the 8-dimension Result Verification Policy Model's actual input document — a well-trodden pattern, not invented from scratch. |
| Workflow | Policy-decision-with-trace evaluation flow | OPA decision logging feature | Reusable as the platform's own audit-trace shape for every Sensitive-Operation authorization decision, not just Result Verification. |
| API Design | OPA's REST Data/Policy API contract shape | OPA | Reference for how the Result Verification Module's internal call to OPA should be structured (input/result/decision-id triplet). |
