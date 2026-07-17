# Readiness for API Platform & Developer Ecosystem Strategy

**Verdict: CONDITIONALLY READY.** API Platform Strategy work may begin
once the conditions below are explicitly acknowledged by whoever owns
that phase — this Board does not itself begin that work (per this
phase's Stop Conditions).

## Why API Strategy Specifically Needs This Baseline

API Platform Strategy will need to define the external contract surface
(REST/GraphQL conventions, versioning policy, SDK generation, developer
portal) sitting on top of the Engines this Baseline freezes. Every
Engine's own API surface (Keycloak's Admin REST API, ERPNext's REST API,
OPA's decision API, Kill Bill's billing API, etc.) is an input the API
Strategy phase must design around, not redesign.

## Readiness Checklist

| Item | Status | Note |
|---|---|---|
| Every Engine's adapter boundary is documented | ✓ Ready | `MASTER_ENGINE_CATALOG.md`'s "Adapter Boundary" column, re-verified in `03-ENGINE-BASELINE.md` |
| No Engine requires API-incompatible platform-side modification (no forks) | ✓ Ready | `06-FORK-BASELINE.md` — zero Controlled Forks |
| Cross-Engine composition patterns are documented (which Engines call which) | ✓ Ready | `MASTER_DEPENDENCY_MATRIX.md`'s proactive-avoidance entries explicitly document composition boundaries (e.g., ERPNext → OpenBoxes, Kill Bill ← OPA) |
| License terms affecting API exposure are known | ⚠ Conditional | AGPL-3.0's network-use clause is directly relevant to how an Engine's functionality may be re-exposed through the platform's own API — API Strategy should not finalize an AGPL-Engine-backed endpoint's terms of service until `08-AGPL-LEGAL-CHECKLIST.md` clears |
| Vendor lock-in assessed for API-surface stability | ✓ Ready | `11-RISKS.md` Task 15 finding — no unacceptable lock-in identified |
| FHIR version pinned for any FHIR-shaped API contract | ⚠ Gap | `11-RISKS.md` R-06 — must be resolved before any FHIR-adjacent public API (e.g., an eventual Patient/Order API) is finalized |
| SaaS Commercial Operations' entitlement model is stable enough to gate API access tiers | ✓ Ready | Kill Bill + OPA composition (`saas-commercial-operations/usage-metering-entitlements/`) is frozen and directly usable as the API-tier-gating mechanism |

## Blocking Items for API Strategy

**None are hard blockers to *starting* API Strategy work.** Two items
are blockers to *finalizing* specific API contracts:

1. R-06 (FHIR version unpinned) — blocks finalizing any clinical-data-
   shaped API endpoint specifically, not the API Strategy phase generally.
2. AGPL legal review outcome — blocks finalizing terms-of-service
   language for any API endpoint that re-exposes an AGPL-licensed
   Engine's functionality (Cal.com, Atlas CMMS, openIMIS, Frappe
   Helpdesk, Frappe CRM), not the API Strategy phase generally.

## Board Recommendation

API Platform Strategy work **may begin**, using `02-TECHNOLOGY-
BASELINE.md` as its technology input, with both conditional items
tracked as explicit dependencies (not silently assumed resolved) on
the endpoints they affect.
