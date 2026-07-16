# Feature: Authorization (RBAC/ABAC)

**Module:** Identity and Access (Platform Kernel)
**Source (Discovery):** Constitution Section 21 (Backend-Enforced
Authorization, Sensitive Operations); Wave 6's **Configurable Result
Verification Policy Model** (8 context dimensions: org type, analysis
type, risk, specialty, approval level, role, branch, country policy, plus
emergency override) — the single most demanding authorization
requirement in the entire platform; Risk Register #20/SEC-07
(unauthorized result verification, Highest severity).

## What This Feature Covers

Two distinct layers, deliberately not conflated:
1. **Coarse-grained RBAC** (can this Role reach this Module/screen at
   all) — a good fit for Keycloak's built-in Role/Group model (same
   Engine as `../authentication/`).
2. **Fine-grained, context-aware ABAC/Policy evaluation** (can *this*
   user verify *this* result, given org type + analysis type + risk +
   specialty + branch + country policy + emergency-override state) — the
   Configurable Result Verification Policy Model's actual requirement,
   which exceeds what a general-purpose IAM's built-in RBAC is designed
   to express well.

This split is itself this Feature's key finding — it is not a
single-engine decision like the rest of this Module.
