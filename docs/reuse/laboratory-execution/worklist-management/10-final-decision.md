**Final Decision: REFERENCE (OpenELIS Global primary, SENAITE secondary)
+ BUILD**

Resolves the decision deferred at Module 12 (`order-entry-cpoe`) and
Module 13 (`specimen-accessioning`). After genuinely weighing wholesale
ENGINE + ADAPTER adoption of SENAITE or OpenELIS Global against the
Core Domain risk, wholesale adoption is **not selected** — both are
complete system-of-record applications, and this Feature sits at the
center of ADR-0011 Amended's Core Domain, the point in the whole chain
where displacing platform ownership would be most damaging, not least.

The platform BUILDs its own Worklist Aggregate, informed by OpenELIS
Global's FHIR-native worklist/Task data shapes (primary Reference,
consistent with the platform's established FHIR convention) and
SENAITE's mature Westgard-rules QC workflow design (secondary Reference,
scoped narrowly to `quality-control-tracking`).

This is not a lower-confidence decision than the Modules that adopted
Engines (Keycloak, OPA, immudb, etc.) — it is a differently-shaped
decision: the evidence supports BUILD precisely because it is Core
Domain, the same class of finding as Patient Management (Module 9), now
confirmed a 5th time with the most direct, closest-to-center case in the
program.
