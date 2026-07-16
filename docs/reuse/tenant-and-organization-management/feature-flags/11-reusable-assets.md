# Reusable Assets — Feature Flags

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| API Design | OpenFeature evaluation API (flag key, context, default value) | CNCF OpenFeature spec | Reusable as the platform's own internal flag-evaluation contract, vendor-neutral by construction. |
| Workflow | 4-eyes change-approval flow for flag changes | Unleash | Directly reusable as a template for the candidate "Elevated Audit" governance tier (Wave 6), beyond just feature flags. |
