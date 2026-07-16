# Architecture Review — Consent Management

Recommended design: model the platform's own Consent Aggregate directly
against the **FHIR `Consent` resource shape** (policy category, scope,
actors, data category, provision period, verification status) — a
Reference, not an Engine, decision. Enforcement (checking consent status
before a data-sharing or AI-processing action proceeds) is platform-owned
logic, evaluated the same way other Sensitive-Operation gates are (Module
1's OPA integration is a candidate reuse point — a consent check is
structurally another attribute in the same kind of policy evaluation
already being built for Result Verification).
