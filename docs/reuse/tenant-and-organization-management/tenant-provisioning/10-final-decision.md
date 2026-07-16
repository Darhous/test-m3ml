# Final Decision — Tenant Provisioning

## Decision: **BUILD** (orchestration layer only; underlying primitives are Reuse)

The Saga itself is platform-specific and correctly built; it calls
already-decided Engines (Keycloak, Module 1; PostgreSQL RLS, this
Module) rather than reinventing identity or isolation primitives. This is
the first Feature in the program to correctly land on BUILD, and it is
evidence-based, not a default — every alternative considered was either
not a real product category (no "tenant onboarding Saga" product exists
for a platform-specific business process) or already covered by prior
decisions.
