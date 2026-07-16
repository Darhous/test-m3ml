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

- Modules fully researched: **3 of 28** (Identity and Access, Tenant and
  Organization Management, Audit and Compliance) — Platform Kernel
  complete
- Features fully researched: **17 of 106** (16 independently researched;
  `document-control` correctly consolidated/deferred, not independently
  researched, per the detected duplicate)
- Repositories evaluated: **17** (adds immudb, Trillian, Eramba, CISO
  Assistant, GovReady-Q, HL7 FHIR Consent resource to the prior 11), all
  logged in `MASTER_REPOSITORY_DATABASE.md`
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
5. **Module 2 (Tenant and Organization Management) directly informs
   `open-questions.md` #15** with real evidence: 2026 industry consensus
   independently converges on the same "tenant-ID-column + Row-Level
   Security" option Discovery Phase 09 had already narrowed to — offered
   as evidence for the eventual SAD decision, explicitly not this
   program silently resolving a Discovery-tracked Open Question on its
   own authority.
6. **Not every Feature resolves to "adopt Product X."** Multi-tenancy
   isolation resolved to REFERENCE (a database-native pattern, not a
   product) and 2 of 5 Features in Module 2 (tenant-provisioning,
   organization-branch-hierarchy) correctly resolved to BUILD — reported
   honestly rather than forcing a product-shaped answer onto every
   Feature.
7. **A second flag/config engine (Flagsmith) was deliberately rejected**
   for the `tenant-configuration` Feature specifically to avoid running
   two flag platforms, even though Flagsmith's own design arguably fits
   that Feature's description slightly better in isolation — a direct,
   evidence-based application of the program's duplicate-elimination
   objective over a locally "better fit."
8. **Platform Kernel now complete (Modules 1–3 of 28).** OPA (Module 1)
   is now confirmed reused across 3 distinct Features in 2 Modules
   (Result Verification authorization, Governance policy-engine, Consent
   enforcement) — the strongest Cross-Feature Dependency case in the
   program so far.
9. **The program's first genuine category-mismatch finding:**
   `consent-management` searched for a "consent management platform" and
   found only website/cookie-consent tools (Klaro-class) — explicitly
   the wrong category for clinical patient consent. Reported honestly
   (REFERENCE the FHIR data model + BUILD enforcement) rather than
   force-fitting an ill-suited product to manufacture a "Buy" answer.
10. **The program's first low-confidence recommendation:**
    `compliance-tracking` (Eramba, tentative) is explicitly flagged as
    needing SAD-level reconsideration — no general-purpose GRC tool is
    healthcare-specific, and licenses need `Requires Legal Verification`.
    Reported as weak evidence rather than dressed up as equally solid.
11. **First detected duplicate Feature across Modules:** Audit and
    Compliance's `document-control` and Document Management's
    `document-control-workflow` are the same capability — research
    correctly deferred rather than duplicated, logged in
    `MASTER_DEPENDENCY_MATRIX.md`'s new "Detected Duplicate Features"
    section.

## Program Pacing — Honest Status (2026-07-16)

One Module (7 Features, 91 files, 6 repositories genuinely researched via
live WebSearch) took a substantial share of a single working session at
full depth. At this measured pace, exhaustively completing all 28 Modules
/ 106 Features / ~1,378 files to the same evidentiary depth is a
multi-session program lasting well beyond this session — consistent with
the pacing note already logged in `MASTER_FEATURE_CATALOG.md`. This is
reported here transparently rather than silently thinning out research
quality in later Modules to appear faster.
