# Open Questions Review

This Board reviewed every Open Question touched by the reuse program
and attempted to close each honestly. Per the No-Guessing Rule, a
question is closed here only if this Board has actual new evidence or
authority to decide it — an Enterprise Architecture Review Board has
neither the product authority nor new market evidence to resolve a
business-strategy or product-scope question. Where that is the case,
the question is left OPEN with explicit justification, not closed by
default.

## Platform-Level Open Questions (from `.claude/context/open-questions.md`)

### #6 — Is Offline Mode required at all?

**Status: REMAINS OPEN.** Directly blocks `home-collection-logistics`
(Specimen Operations) past the architecture-pattern level
(`specimen-operations/home-collection-logistics/10-final-decision.md`).

**Why this Board does not close it:** This is a product/business-
requirement question ("does the platform need to support field agents
working without connectivity?"), not a technology question. No Engine,
Library, or architecture evidence this Board reviewed bears on whether
the *requirement* exists — only on how to *satisfy* it if confirmed
(the reuse program's own Reference note: a local-first-capture +
eventual-sync pattern, PouchDB/CouchDB-class). Closing this would
require product-owner input this Board does not have and is not
authorized to substitute its own judgment for.

**Justification for leaving OPEN:** No-Guessing Rule (`CLAUDE.md`
Section 3) — asserting an answer without confirmed input would be
exactly the failure mode the project's Context Store discipline exists
to prevent.

**Resolved 2026-07-18 (Open Questions Resolution):** the product owner
(the user) confirmed Offline Mode is Required (D-48). This entry is
preserved as the accurate record of why this Board could not close it —
see `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md` for the
resolution and `docs/certification/25-PRE-SAD-CLEAN-CLOSURE.md` for
confirmation that 0 architectural blockers remain.

### #14 — What is the platform's Core Domain? (ADR-0011)

**Status: REMAINS OPEN at the ADR level** (`Proposed — Amended`, not
`Accepted`) **but this Board confirms the reuse program's *use* of the
Proposed answer as its working assumption was appropriate and internally
consistent.**

See `10-ADR-REVIEW.md` for the full ADR-0011 review. In summary: the
reuse program correctly treated "Patient-to-Result Orchestration" as the
best-available working hypothesis for Core Domain preservation decisions
(rejecting OpenMRS, Bahmni, SENAITE, OpenELIS Global, openIMIS as
wholesale replacements across 7 Modules) without ever asserting the ADR
itself was Accepted. This Board finds no instance where a reuse decision
silently treated ADR-0011 as more settled than it actually is.

**This Board does not close Open Question #14** — it requires the same
user business-strategy input as #6, specifically resolution of the
documented "Specimen Management" competing alternative (ADR-0011's own
"Alternatives Considered" section). This is squarely outside an
architecture review board's authority.

### #15 — Exact shared-tier tenant-partitioning technology (tenant-ID column vs. schema-per-tenant)

**Status: REMAINS OPEN**, with reuse-program evidence now formally
logged toward (not resolving) the answer.

The reuse program's Module 2 research (`tenant-and-organization-
management/multi-tenancy-isolation/`) found that PostgreSQL Row-Level
Security (tenant-ID-column approach) represents 2026 industry
consensus for this class of platform — directly corroborating Discovery
Phase 09's own narrowing to the same 2 candidate approaches
(`docs/discovery/artifacts/09-tenancy-analysis.md`). **This Board
confirms that evidence is real and should carry forward to the SAD**,
but does not itself select between tenant-ID-column and schema-per-
tenant — that is explicitly an SAD-level decision per Constitution v1's
own framing of this question, not an EARB-level one.

**Justification for leaving OPEN:** the question was explicitly deferred
to the SAD by the Constitution itself, not by this Board's choice.

### #16 — Tenant promotion-path trigger (shared → dedicated tier)

**Status: REMAINS OPEN.** No reuse-program Feature addressed this
question directly (it is a tenancy-lifecycle policy question, not a
Build-vs-Buy one). No new evidence to log. Unchanged from Discovery
Phase 09's own finding: a trigger *type* was proposed (measured resource
consumption or contractual/regulatory requirement) without a specific
threshold — inventing a number here would violate the No-Guessing Rule
identically to the original Discovery finding.

## Reuse-Program-Internal Open Items (Not in `open-questions.md`, but Carried Forward from `docs/reuse/`)

These are not formally tracked platform-level Open Questions, but the
reuse program itself flagged them as unresolved — this Board reviews
each for closability.

### Eramba Community's `compliance-tracking` confidence level

**Status: REMAINS OPEN / CONDITIONALLY APPROVED.** The reuse program
explicitly logged this as its lowest-confidence decision
(`audit-and-compliance/compliance-tracking/10-final-decision.md`).
This Board attempted to close it by checking whether any later Module
surfaced a stronger alternative — none did (Quality Management, Module
16, searched adjacent territory for CAPA/complaint tooling and also
found no credible healthcare-specific GRC/compliance product). **This
Board cannot close this with higher confidence than the original
finding** — doing so would require new market research this phase's
scope explicitly excludes ("Do NOT perform another market scan unless
absolutely necessary to verify a blocker"). This Board judges Eramba's
status is not itself a blocker (a working Engine is adopted, just at
lower confidence) and therefore does not trigger the "absolutely
necessary" exception. Left CONDITIONALLY APPROVED, reconsider at SAD.

**Update (2026-07-18, Final Pre-SAD Semantic Consistency Correction):**
"reconsider at SAD" is preserved as this Board's own original finding,
but it is superseded — the SAD is not a vendor-selection phase, so a
frozen Baseline entry cannot carry an instruction to informally
reconsider it during SAD authoring. Eramba remains conditionally
approved; the SAD documents the selection and its due-diligence gate
without comparing or selecting a replacement. See `02-TECHNOLOGY-
BASELINE.md` (E5) and `docs/certification/
26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`.

### Novu and Documenso license strings (never independently confirmed)

**Status: CLOSABLE only by direct verification, not by this Board's
review.** Reading an actual LICENSE file is a mechanical, low-risk
action this Board could in principle take without violating "no market
scan" (it is not a re-scan of alternatives, just reading one file). This
Board elected **not** to perform even this narrow check in this pass,
to preserve a clean separation between "architectural ratification"
(this phase) and "legal-text verification" (explicitly assigned to
formal legal review in `08-AGPL-LEGAL-CHECKLIST.md`). Left OPEN,
assigned as checklist items 6-7.

### Mirth Connect's frozen-release status

**Status: NOT an Open Question — a confirmed, standing Risk.** This is
not an unresolved question awaiting evidence; it is a fully-understood,
already-evidenced fact (NextGen's March 2025 commercial shift) with a
known mitigation (Apache Camel fallback). Carried into `11-RISKS.md`
R-02, not listed as Open here to avoid conflating "we don't know" with
"we know and are managing it."

## Board Summary

| Question | Status | Closable by This Board? |
|---|---|---|
| #6 — Offline Mode | OPEN | No — product/business question |
| #14 — Core Domain (ADR-0011) | OPEN | No — product/strategy question |
| #15 — Tenant partitioning technology | OPEN | No — explicitly deferred to SAD |
| #16 — Tenant promotion trigger | OPEN | No — no new evidence exists |
| Eramba confidence | OPEN (conditional) | No — would require a new market scan, out of scope |
| Novu/Documenso license | OPEN | Partially — assigned to legal checklist, not resolved here |

**Total remaining Open Questions: 6** (4 platform-level + 2
reuse-program-internal). **Zero were closed by this Board** — every one
requires either product/business authority or formal legal action this
Board does not hold. This is reported honestly as the correct outcome,
not a shortfall: an architecture review board fabricating closure on a
business-strategy or legal question would be a more serious governance
failure than leaving it accurately open.
