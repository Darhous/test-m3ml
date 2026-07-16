# Architecture Review — Policy Engine

The same OPA instance/deployment already selected for Result Verification
(Module 1) is reused here for the broader candidate "Elevated Audit" tier
policies (Refund, Expiry-block, Break-Glass, Tenant Configuration) once
`open-questions.md` #24 is resolved — additional Rego policy bundles, not
a new engine. This directly demonstrates the program's Cross-Feature
Dependency principle a second time (OPA now serves 2 Modules).
