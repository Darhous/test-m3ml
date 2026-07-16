# Integration Options — Feature Flags

Recommended: adopt the platform's own evaluation code against the
**OpenFeature** SDK/API (vendor-neutral), with Unleash as the backing
provider. This means a future switch to Flagsmith (or any other
OpenFeature-compatible provider) would not require rewriting flag-
evaluation call sites across the codebase — directly serving this
program's own "bounded exit path" principle (same discipline already
applied to the OIDC-standard choice in Module 1). Flags are evaluated
using the same Organization ID propagated from Keycloak (Module 1) and
the same `tenant_id` used by RLS (this Module's `multi-tenancy-isolation`
Feature) — one consistent tenant-identity thread through the whole
platform.
