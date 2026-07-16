# Master Executive Summary — Global Build-vs-Buy & Reuse Intelligence Program

**Status: In Progress.** This document is updated at the end of every
completed Module and rewritten in full at program completion. See
`MASTER_FEATURE_CATALOG.md` for the authoritative scope (28 Modules, 106
Features) and per-Feature research status.

## Program Framing

The objective is to minimize implementation effort on the Healthcare
Operations Platform (`docs/discovery/HEALTHCARE-OPERATIONS-DISCOVERY-BOOK.md`)
before any Software Architecture Document work begins, by identifying,
for every Feature, whether to Build, Fork, wrap an Engine, adopt an SDK,
adopt a Library, reuse a Reference design, or Reject a candidate — with
every recommendation evidence-based (real repositories, real license
text, real security/community signal), never GitHub-stars-ranked, never
invented.

## Scale and Pacing (read this first)

28 Modules × 106 Features × 13 required files per Feature = **~1,378
individual documents**, each requiring genuine, live, per-candidate
research (repository inspection, license text, security history,
community signals). This cannot be done shallowly and quickly at the
same time — the program's own Quality section explicitly forbids
shallow research, GitHub-top-stars lists, and guessing. This program
therefore executes as a **Module-by-module marathon**, one Module fully
researched, decided, and committed at a time, continuing across sessions
until every Stop Condition is met. This section is updated with running
totals after every Module.

## Priority Order and Rationale

Modules are researched in an order chosen to front-load the highest
effort-savings-per-hour-invested first, per the program's own "if it can
save 1000 hours, reuse it" directive — not in arbitrary catalog order:

1. **Identity and Access** — universal dependency (Platform Kernel,
   Wave 10), every other Module needs it, and mature enterprise-grade
   open-source answers exist (Keycloak-class IAM) that would otherwise
   cost the single largest amount of avoidable engineering effort on the
   entire platform if built from scratch.
2. **Laboratory Execution / Specimen Operations / Result Verification and
   Reporting** — the Core Domain cluster (ADR-0011, Amended) and the
   single deepest, most mature open-source category available (SENAITE,
   OpenELIS Global, Bika LIMS) — the platform's own competitive
   differentiation lives here, so these decisions carry outsized
   architectural weight even though the Core Domain itself will likely
   see the least code reuse (highest customization need).
3. **Tenant and Organization Management, Audit and Compliance** — the
   remaining Platform Kernel, needed before any Business Module can be
   meaningfully scoped for reuse (isolation and audit posture constrain
   every subsequent candidate's suitability).
4. **Device Integration Gateway, Notification Service, AI Operations
   Gateway** — Shared Infrastructure (Independent Components per ADR
   0006/0007), each with strong existing OSS categories (HL7/FHIR
   integration engines, notification-orchestration platforms, LLM
   gateways).
5. Remaining Business Modules and the Commercial Module, in the
   Feature Catalog's listed order, since no single one carries the same
   universal-dependency or Core-Domain weight as groups 1–4.

## Running Totals

*(Updated after every Module — see individual Module completion notes
for the detailed count.)*

- Modules fully researched: **1 of 28** (Identity and Access)
- Features fully researched: **7 of 106**
- Repositories evaluated: **6** (Keycloak, OPA, Zitadel, Authentik, Ory
  Kratos+Hydra, Casbin), all logged in `MASTER_REPOSITORY_DATABASE.md`
- Estimated total effort-hours identified as reusable: **not numerically
  estimated** — no invented number, per the No-Guessing Rule; the
  qualitative conclusion (universal-dependency Feature, mature enterprise-
  adopted Engine, lowest-scoring alternative was Build In-House on nearly
  every dimension) is the evidence-based basis for the decision instead.

## Key Findings So Far

1. **Identity and Access is almost entirely a single-Engine decision.**
   6 of the Module's 7 Features are solved by one repository (Keycloak),
   demonstrating the program's own Cross-Feature Dependency Map principle
   directly — most of this Module's research effort front-loaded into the
   `authentication` Feature, with the remaining 5 Keycloak-solved
   Features requiring only differential analysis.
2. **One genuine second-engine case found:** the Configurable Result
   Verification Policy Model's 8-dimension, Sensitive-Operation-grade
   requirement (Discovery Wave 6) is architecturally too demanding for
   Keycloak's built-in RBAC — Open Policy Agent (CNCF Graduated) is the
   evidence-based answer, integrated narrowly (only the Result
   Verification and Reporting Module calls it), not platform-wide.
3. **License due diligence changed a ranking**, not just a footnote:
   Zitadel scored competitively on architecture but Keycloak was
   preferred partly because Zitadel's 2025 shift to AGPL 3.0 introduces a
   real (if manageable) licensing complication for a White-Label
   multi-tenant commercial SaaS product — exactly the kind of finding
   this program exists to surface before the SAD, not after.
4. **This Module's adoption does not resolve Discovery's Highest-severity
   open risk** (Risk Register #17/SEC-04, shared-tier tenant partitioning,
   `open-questions.md` #15) — Keycloak's Organizations feature is
   compatible with either resolution but does not itself decide it. Named
   explicitly so a future reader does not mistake tooling adoption for
   architectural decision-making.

## Program Pacing — Honest Status (2026-07-16)

One Module (7 Features, 91 files, 6 repositories genuinely researched via
live WebSearch) took a substantial share of a single working session at
full depth. At this measured pace, exhaustively completing all 28 Modules
/ 106 Features / ~1,378 files to the same evidentiary depth is a
multi-session program lasting well beyond this session — consistent with
the pacing note already logged in `MASTER_FEATURE_CATALOG.md`. This is
reported here transparently rather than silently thinning out research
quality in later Modules to appear faster.
