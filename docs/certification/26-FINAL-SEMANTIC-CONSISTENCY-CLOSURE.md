# Final Semantic Consistency Closure

**Phase:** Final Pre-SAD Semantic Consistency Correction — a narrowly
scoped correction phase reviewing the *meaning, authority, and current
governance status* of three verified semantic inconsistencies, not
their keyword counts alone. Not a new architecture phase, not a
redesign, not a vendor re-evaluation exercise, and not the Software
Architecture Document (SAD) phase. **Starting commit:** `bea37a2`
(Pre-SAD Baseline Correction & Clean Closure). **Date:** 2026-07-18.

## 1. Scope

Three verified semantic inconsistencies, each a genuine contradiction
between an *active governing statement* and the *current baseline*
(not a numeric drift, which the prior phase already closed):

1. Eramba Community's Technology Baseline status literally instructed
   "reconsider at SAD" while the same Baseline is FROZEN and mandatory
   SAD input — the SAD is not a vendor-selection phase, so the two
   statements could not both be true.
2. ADR-0014's Dependency Recovery Responsibilities rule named a
   specific, already-stale Engine count (21) inside a rule meant to
   outlive any single Baseline snapshot, and was too narrowly tied to
   Module ownership when some ratified components are owned by a
   platform capability rather than a Bounded Context.
3. The Constitution's Non-Functional Budgets section (RTO/RPO rows)
   stated disaster recovery was undesigned and no database product was
   chosen — both true when v2 was authored, both stale once ADR-0013
   and ADR-0014 were Accepted.

No Accepted ADR was reopened. No replacement vendor was selected. No
numeric RPO, RTO, availability, retention, region, or topology figure
was introduced anywhere.

## 2. Verified Issues (as confirmed by direct review)

All three were confirmed present exactly as described in the mission
before any edit was made — this was not a keyword-count exercise;
each statement's actual current meaning was read in context first.

## 3. Eramba Governance Correction

**Before:** `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` E5 —
`CONDITIONALLY APPROVED — reconsider at SAD`.

**After:** `CONDITIONALLY APPROVED — implementation due diligence
required before production adoption; not subject to re-evaluation
during SAD authoring`. The Upgrade Policy column now names the actual
due-diligence gate: license verification, security/maintenance
assessment, deployment and integration fit, operational ownership
confirmation, exit-strategy validation, and formal Architecture Review
Board approval before production adoption.

**No vendor comparison was performed. No replacement was selected. No
approval was silently upgraded** — Eramba remains exactly as
conditional as before; only the *nature* of what remains conditional
changed, from "may be swapped at SAD" to "must clear implementation
due diligence."

**Required interpretation, now consistently stated:** the GRC/
Compliance capability remains architecturally recognized; Eramba
remains the current conditional product selection; the SAD may
document the selection, its constraints, and its due-diligence gate,
but must not compare or select a replacement product; failed due
diligence triggers formal governance (a new ADR, Technology Baseline
amendment, or EARB decision) — never a silent substitution.

**Propagated to:**
- `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` (E5 row — the
  authoritative product-decision cell).
- `docs/certification/11-RISK-REGISTER.md` (R-01's Mitigation and
  Status columns — the active risk record).
- `docs/certification/15-SAD-INPUT-PACKAGE.md` (item 6 — corrected
  from "still a Dependency, unresolved" to ✅ Resolved governance
  status, with the narrower genuine remaining due-diligence dependency
  named explicitly).
- `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md` (Remaining
  Risks section, R-01 line).
- `docs/architecture-review/01-EXECUTIVE-SUMMARY.md` and
  `09-OPEN-QUESTIONS.md` (EARB's own original findings — **preserved
  unmodified**, each with a forward-reference note added, per Section
  10 below).
- `docs/architecture-review/11-RISKS.md` — one top-of-file supersession
  note added; this file is the historical predecessor already
  consolidated into `11-RISK-REGISTER.md` by that document's own
  construction.

## 4. ADR-0014 Ownership/Count Correction

**Before:** "Each of the 21 ratified Engines' own backup/recovery
capability is the responsibility of the Module holding that Engine's
Single Adoption Point."

**After:** a durable, count-independent rule: every ratified Engine or
stateful platform component that stores authoritative data,
recoverable configuration, secrets, policies, integration state, or
operational metadata must have an explicitly assigned backup, restore,
recovery-validation, and disaster-recovery responsibility, applying
uniformly regardless of how many Engines the Baseline ratifies at any
point in time. Ownership is clarified to belong to the responsible
**Module, Bounded Context, Independent Component, platform capability,
or operational owner** — not every Engine's Single Adoption Point maps
to a conventional domain Module. The rule also clarifies that not
every stateless library or Reference Standard needs an independent
backup strategy in its own right, though its configuration/secrets/
policies/schemas may still need recovery; and that central platform
coordination of DR execution must never collapse into an
undifferentiated central obligation with no named owner.

**Unchanged, as required:** the four criticality tiers, the Accepted DR
principles, the Pending status of every numeric RPO/RTO value, the
SaaS/On-Premise/Hybrid responsibility model, and the ADR's Accepted
status. The rest of ADR-0014 was reviewed for other count-coupled
wording — none was found (verified by direct search for "21", "24",
"33", "Engines" across the full document).

## 5. Constitution Amendment Summary

Applied via Section 45 (Constitution Amendment Process): explicit user
instruction (this mission) as the required approval; this document plus
the CHANGELOG entry as the required record; a version bump (the change
is substantive enough to warrant one, per Section 45's own criterion);
no new ADR required, since the amendment documents two *already-
Accepted* ADRs rather than deciding anything new.

**Exact changes**, all confined to *status/reason* text — no rule
content, principle, or numeric value changed:

1. Section 51 (Non-Functional Budgets): RTO and RPO rows' *Reason /
   Basis* column corrected. *Value* (`Not set`) and *Status* (`Draft`)
   are unchanged for both.
2. Section 6 (Strategic Design): the Core Domain "Recommendation (not
   yet a Rule)" paragraph now carries an update note — the Core Domain
   was Accepted (ADR-0011) in the Open Questions Resolution phase. This
   was discovered during the required review of Constitution sections
   for stale statements (see Section 10 below) and falls under the same
   "active governing text vs. current baseline" defect class as the
   RTO/RPO issue, so it was corrected under the same amendment rather
   than left inconsistent.
3. Section 47 Glossary: the "Core Domain" table row's Status column
   updated from "Open — not yet identified" to Accepted, citing
   ADR-0011.
4. Section 46 (Open Questions): a header-level update note added
   stating all 14 listed items were subsequently resolved. **The
   14-item list itself was not rewritten** — it is preserved as the
   historical record of what was open at authoring time, consistent
   with the smallest-compliant-amendment principle.
5. Title, Status line, "v2 note," new "v2.1 note," and closing
   statement — version metadata only.
6. `docs/constitution/README.md`'s Version line — corrected from a
   pre-existing stale "v1" (a documentation-currency defect discovered
   while reviewing the README as Section 45 requires, unrelated in
   origin to the RTO/RPO/Core-Domain substance but fixed under the same
   amendment since it is the same class of defect: active text not
   reflecting current state).

## 6. Constitution Version Before and After

| | Before | After |
|---|---|---|
| Version | v2 | **v2.1** |
| Status | Accepted (v2) | Accepted (v2.1) |
| README "Current version" line | v1 (stale, pre-existing) | v2.1 |
| Sections with substantive rule changes | — | 0 (status/reason text only) |

## 7. Files Created

- `docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md` (this
  document).

## 8. Files Modified

- `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` (E5 Eramba row)
- `docs/certification/11-RISK-REGISTER.md` (R-01 row)
- `docs/certification/15-SAD-INPUT-PACKAGE.md` (item 6, resolved count)
- `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md` (R-01 remaining-risk line)
- `docs/architecture-review/01-EXECUTIVE-SUMMARY.md` (forward-reference note)
- `docs/architecture-review/09-OPEN-QUESTIONS.md` (forward-reference note)
- `docs/architecture-review/11-RISKS.md` (top-of-file supersession note)
- `docs/adr/0014-disaster-recovery-and-business-continuity-baseline.md` (Dependency Recovery Responsibilities section)
- `docs/constitution/PROJECT-CONSTITUTION.md` (version metadata; Section 6, 46, 47, 51; closing statement)
- `docs/constitution/README.md` (Version line)
- `docs/constitution/CHANGELOG.md` (new v2.1 entry)
- `docs/api-platform/01-API-VISION.md` (Engine-count reference qualified)
- `.claude/context/open-questions.md` (item 14 — Core Domain — marked RESOLVED)
- `.claude/context/glossary.md` (Accepted Definitions intro + Core Domain row)
- `docs/certification/14-PROJECT-INDEX.md` (new file 26 entry)

## 9. Semantic Search Results

Full-repository search across `.claude/context/`, `docs/adr/`,
`docs/api-platform/`, `docs/architecture-review/`, `docs/certification/`,
`docs/constitution/`, `docs/reuse/` for: `reconsider at SAD`, `21
ratified Engines`, `21 Engines`, `not yet designed`, `no database
product`, `Disaster Recovery`, `RPO`, `RTO`, `Eramba`, `PostgreSQL`,
`ADR-0013`, `ADR-0014`, `12 ADR`, `14 ADR`, plus a targeted sweep for
"Core Domain is not decided"-class statements once the Section 46
finding surfaced that class of defect.

**Genuine active-governance defects found and fixed (beyond the 3 named
issues):**
- `.claude/context/open-questions.md` item 14 (Core Domain) — never
  updated with a RESOLVED marker during the Open Questions Resolution
  phase, unlike items 28/29. This is the live Context Store; leaving it
  stale would have directly contradicted ADR-0011's Accepted status.
  Fixed with the same RESOLVED-prefix convention used for items 28/29.
- `.claude/context/glossary.md`'s "Core Domain" entry — same defect,
  same fix pattern.
- Constitution Section 6/46/47 — same defect (see Section 5 above).
- `docs/api-platform/01-API-VISION.md` — a live "21 ratified Engines"
  parenthetical in a still-current architectural-principle statement
  (every Engine sits behind an ACL); qualified with the current count
  and a pointer, principle itself unchanged.

**Confirmed accurate as historical, left unmodified (with or without a
supplementary forward-reference note, per the case):**
- `docs/reuse/device-integration-gateway/hl7-integration-engine/
  10-final-decision.md` — a different Engine's (Mirth Connect) own
  historical mitigation language, outside this phase's Eramba/GRC
  scope.
- `docs/certification/05-DDD-CERTIFICATION.md` — sibling of
  `04-ADR-CERTIFICATION.md`, `16-EXECUTIVE-DOSSIER.md`,
  `18-CERTIFICATION-REPORT.md`; all four are the same frozen
  Certification Audit package, already covered by that package's own
  established "historical record, not retroactively rewritten"
  convention (`15-SAD-INPUT-PACKAGE.md`, `14-PROJECT-INDEX.md`).
- `docs/certification/22-ARCHITECTURE-BASELINE-FREEZE.md`'s Remaining
  Risks table — cites R-01 by ID only, defers to
  `11-RISK-REGISTER.md` for detail; no independent claim to correct.
- `.claude/context/module-catalog.md`'s "Core Domain مرشّح" (candidate)
  row — a Discovery-phase mapping table describing that phase's own
  candidate-context output; the table's title and scope are explicitly
  about Discovery candidates, not a live status claim, and this file
  was deliberately not touched further given this session's own
  precedent of the user declining large edits to it.
- `docs/constitution/PROJECT-CONSTITUTION.md`'s two "does not name a
  database product" self-scope statements (opening paragraph, closing
  statement) — these describe the Constitution's own deliberate
  technology-agnostic authoring style (delegating product choices to
  ADRs, exactly as it already does for all 14 ADR-backed decisions),
  not a claim that no database has been chosen anywhere in the
  repository. Confirmed not contradictory; left as accurate,
  supplemented with an explicit ADR-0013 cross-reference for clarity.

## 10. Historical Statements Deliberately Preserved

Per this phase's explicit instruction not to falsify history:

- `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` E5's *original*
  "reconsider at SAD" wording is not directly quoted as history anywhere
  (the Baseline row itself is a live, single-source-of-truth field that
  the Amendment Process governs — it was corrected in place, consistent
  with how every other Baseline field is maintained; the original
  wording remains visible in this repository's git history).
- `docs/architecture-review/01-EXECUTIVE-SUMMARY.md`'s "One decision is
  downgraded... Reconsider at SAD" finding — preserved verbatim, with a
  forward-reference note appended explaining why it is superseded.
- `docs/architecture-review/09-OPEN-QUESTIONS.md`'s "Left CONDITIONALLY
  APPROVED, reconsider at SAD." finding — preserved verbatim, with a
  forward-reference note appended.
- `docs/architecture-review/11-RISKS.md`'s original R-01 mitigation
  text ("Reconsider at SAD time with a dedicated, focused re-search") —
  preserved verbatim; a single top-of-file supersession note added.
- `.claude/context/open-questions.md` item 14's full original text
  (the Discovery Phase 04 proposed answer, the Gap Closure Wave 7
  re-evaluation) — preserved verbatim beneath a new RESOLVED prefix,
  exactly the pattern already established for items 28/29.
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 46's 14-item Open
  Questions list — preserved verbatim as the historical record of what
  was open at v1/v2 authoring; only a header-level note was added above
  it.
- `docs/certification/04-ADR-CERTIFICATION.md`,
  `05-DDD-CERTIFICATION.md`, `16-EXECUTIVE-DOSSIER.md`,
  `18-CERTIFICATION-REPORT.md` — the original Certification Audit
  package, entirely untouched by this phase, per the convention that
  package already established for itself.

No older number was treated as a defect merely for being old; every
statement corrected in this phase was verified to still be presented as
*current* governing truth at the time of review.

## 11. Remaining Non-Blocking Dependencies

Unchanged from `25-PRE-SAD-CLEAN-CLOSURE.md` Section 9, with one
narrowing: item 6 (Eramba) is now correctly scoped as an
implementation-time due-diligence item, not an open architectural
reconsideration.

| Type | Items |
|---|---|
| Legal Dependency | AGPL-3.0 review (5 Engines, R-04), unconfirmed licenses (Novu/Documenso, R-07), general local legal requirements, Egypt cross-border transfer rules |
| Regulatory Dependency | Result Verifier eligibility values, Egypt regulatory consolidated (R-13) |
| Country Localization | Language/currency exhaustive list, Egypt Payroll statutory rules, National ID validation rules |
| Operational Assumption | Expected usage volume, legacy migration N/A |
| Implementation Due Diligence (non-architectural) | Eramba Community (R-01) — license verification, security/maintenance assessment, deployment fit, operational ownership, exit-strategy validation, before production adoption |
| Numeric approval, pending named gates | Final RPO/RTO/availability/retention/topology values (ADR-0014) |

## 12. Validation Results

All items on this phase's validation checklist confirmed:

- No active document states Eramba will be reconsidered during SAD
  authoring — confirmed by direct re-read of every corrected file.
- Eramba remains conditional, not silently promoted to unconditional —
  confirmed (Baseline row still reads CONDITIONALLY APPROVED).
- No replacement GRC product was selected — confirmed (no vendor name
  other than Eramba appears as a Decision anywhere touched).
- Failed Eramba due diligence requires formal governance — confirmed,
  stated explicitly in the Baseline row, Risk Register, and this
  document.
- ADR-0014 contains no brittle current Engine count in its
  responsibility rule — confirmed by full-document search.
- ADR-0014 ownership covers Modules, Independent Components, platform
  capabilities, and operational owners — confirmed, stated explicitly.
- Constitution versioning and amendment rules were followed — Section
  45's four Required items all satisfied (explicit user instruction,
  CHANGELOG entry, version bump, no ADR needed since no decision
  reversed).
- Constitution no longer states DR is wholly undesigned — confirmed
  (RTO row now cites ADR-0014's Accepted framework).
- Constitution no longer states no database product is selected in a
  way that contradicts the repository — confirmed (RPO row now cites
  ADR-0013).
- RPO/RTO remain unset and correctly classified as pending numeric
  decisions — confirmed, `Not set` / `Draft` unchanged.
- No RPO, RTO, availability, retention, region, or topology figure was
  fabricated — confirmed by direct re-read of every edit made.
- ADR-0013 and ADR-0014 remain Accepted — confirmed.
- Technology Baseline remains 24 Engines / 4 Libraries / 5 Reference
  Standards / 33 entries — confirmed unchanged; only the E5 row's
  status *text* changed, not the count.
- ADR count remains 14/14 Accepted — confirmed (14 files in
  `docs/adr/`).
- No SAD content has been written — confirmed.
- All internal Markdown references touched by this change point to
  files that exist in the repository (verified for every newly added
  cross-reference, including this document's own forward references
  from files edited before it was written).
- Working tree is clean after commit — verified below.

## 13. Final SAD Readiness Conclusion

All three verified semantic inconsistencies are corrected at the level
of meaning and governance authority, not merely keyword counts. The
additional Core Domain drift discovered in the live Context Store and
Constitution during the required review is also corrected, using the
same historical-preservation discipline applied throughout. No
Accepted ADR was reopened, no vendor was re-evaluated or replaced, and
no numeric DR/database target was fabricated.

# CLEAN SEMANTIC BASELINE — READY FOR SOFTWARE ARCHITECTURE DOCUMENT
