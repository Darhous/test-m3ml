# Integration Options — Authorization (RBAC/ABAC)

## Two-Layer Architecture (Recommended)

1. **Coarse RBAC** — Keycloak Roles/Groups (already adopted, `../
   authentication/`) gate Module/screen-level access ("can this user
   reach the Result Verification and Reporting Module at all").
2. **Fine-grained ABAC/Policy** — OPA evaluates the Configurable Result
   Verification Policy Model's 8-dimension rules at the point of the
   `ResultVerified` command (Wave 5/6), called as a sidecar or library
   from the Result Verification and Reporting Bounded Context (Wave 9,
   Context 7, the Core Domain) — **not** called generically from every
   Module, keeping the integration surface owned by the one Module that
   actually needs this depth (Constitution Section 8).

## Why Not OPA Everywhere

Deploying OPA as the *only* authorization mechanism platform-wide would
be over-engineering for Modules that only need simple Role gates —
consistent with this program's "don't rebuild/over-adopt beyond
documented need" principle. OPA is scoped specifically to Sensitive-
Operation-grade decisions (Result Verification today; the candidate
"Elevated Audit" tier from `open-questions.md` #24, if Confirmed, would
be the next natural OPA consumer).

## Data Flow

`ResultVerified` command received → Result Verification Module calls OPA
with input document (actor attributes from Keycloak token + result
context: org type, analysis type, risk, specialty, branch, country
policy, emergency-override flag) → OPA returns allow/deny + decision
trace → Module logs the full decision trace to the Audit and Compliance
Module (Constitution Section 21+23 combined requirement) → command
proceeds or is rejected.
