# Skills and MCP Review

Part of the Enterprise Architecture Certification Audit (pre-SAD final
quality gate). This document consolidates, verifies, and extends the
Skill/MCP disclosures already made in `.claude/SKILLS-INVENTORY.md`,
`.claude/SKILLS-VALIDATION-REPORT.md`, `docs/api-platform/
00-SKILLS-AND-TOOLS-USED.md`, and `docs/api-platform/32-SKILLS-REPORT.md`
— it does not repeat their full content, it audits whether those
disclosures are accurate, current, and complete as of this audit.

## Installed Skills — Verified Inventory (9)

Re-verified by direct `ls .claude/skills/` at audit time: **unchanged**
from the original 2026-07-15 installation. All 9 skills present, with
their original provenance intact in `.claude/SKILLS-INVENTORY.md`.

| # | Skill | Source | License | Scripts | Version/Commit Pinned | Verified Purpose | Should It Have Been Used? | Was It Used? | Should It Be Used for This Audit? |
|---|---|---|---|---|---|---|---|---|---|
| 1 | `doc-coauthoring` | anthropics/skills | Apache-2.0 | none | `9d2f1ae1` | Structured 3-stage doc co-authoring workflow | Optional — useful for live human iteration, not a single-pass Board deliverable | No (Part 1, Part 2, this audit) | No — this audit is a single-pass certification output, not an iterative co-authoring session |
| 2 | `architecture-patterns` | wshobson/agents | MIT | none | `b6af3711` | Clean/Hexagonal Architecture, DDD tactical patterns | Yes, for contract/layering design | Yes (API Platform Part 2) | Not directly, but its layering discipline underlies this audit's DDD Certification section |
| 3 | `architecture-decision-records` | wshobson/agents | MIT | none | `b6af3711` | ADR templates, lifecycle, review checklist | Yes, for every ADR-touching phase | Yes (EARB, API Platform Parts 1-2) | **Yes — used this audit for ADR Certification (`04`)** |
| 4 | `api-design-principles` | wshobson/agents | MIT | 1 non-executed reference template | `b6af3711` | REST/GraphQL design standards | Yes, for API Platform phases | Yes (API Platform Parts 1-2) | Referenced for API Certification (`06`) consistency checks |
| 5 | `stride-analysis-patterns` | wshobson/agents | MIT | none | `b6af3711` | STRIDE threat identification | Yes, for API Security | Yes (API Platform Part 1) | Referenced for Security Certification (`07`) |
| 6 | `threat-mitigation-mapping` | wshobson/agents | MIT | none | `b6af3711` | Threat-to-control mapping | Yes, for Webhooks/security depth | Yes (API Platform Part 2) | Referenced for Security Certification (`07`) |
| 7 | `c4-architecture` | softaworks/agent-toolkit | MIT | none | `3027f20f` | C4 model Mermaid diagrams | Optional — useful for new system contexts | Yes (API Platform Part 2: Developer Portal, Marketplace) | Not needed — this audit produces no new system context |
| 8 | `mermaid-diagrams` | softaworks/agent-toolkit | MIT | none | `3027f20f` | General diagram generation | Optional | Yes (API Platform Part 2) | Not needed — this audit is text/table-form certification, not diagram-form |
| 9 | `domain-driven-design` | wondelai/skills | MIT | none | `326b3801` | Strategic + tactical DDD | Yes, throughout | Yes (API Platform Parts 1-2) | **Yes — used this audit for DDD Certification (`05`)** |

**Finding: all 9 Skills' provenance records remain accurate.** No
version drift detected (Skills are static file copies, not
auto-updating). No Skill's license, source, or security posture has
changed since installation.

## Skills Discovered But Not Installed — Re-Verified Still Correctly Deferred/Rejected

| Skill | Original Disposition | Still Correct? |
|---|---|---|
| `skill-creator` | Deferred — no need to build a custom skill | Yes — this audit did not need a custom skill |
| `docx` | Deferred — reserved for final export stage | Yes — no export requested this phase |
| `pdf` | Deferred — reserved for final export stage | Yes — no export requested this phase |
| `microservices-patterns` | Deferred — avoids biasing toward microservices, Modular Monolith First is the Accepted direction (ADR-0001) | Yes — still correctly deferred; this audit's DDD Certification confirms no module has since justified extraction |
| ForceInjection DDD pipeline, v3-ddd-architecture, Claude-Code-Skill-DDD (PyPI), antigravity DDD bundle | Rejected at installation (too heavy / unrelated framework / atypical distribution / biases toward event-sourcing) | Yes — no new evidence surfaced this audit that would reverse these rejections |

## New Skills/MCPs Searched For This Audit

Per this phase's mandate to search for additional enterprise capabilities
(Repository Analysis, Compliance, Knowledge Graph, Traceability,
Enterprise Modeling, QA Skills), this Board checked the currently
available skill listing surfaced by the harness at the start of this
turn. Findings:

| Candidate Category | Found in Available Listing? | Disposition |
|---|---|---|
| Repository/codebase analysis | `Explore`/`general-purpose` Agent types (not Skills) already provide this; no dedicated "Repository Intelligence Skill" found | Not installed — existing Agent tooling covers this audit's actual need (used 3 parallel Explore/general-purpose agents for `docs/reuse/` and `docs/discovery/` consistency verification, see Method note below) |
| Compliance/Governance Skill | None found beyond what `architecture-decision-records` + this project's own Constitution Sections 56-62 already cover | Not installed — no gap found; this project's own governance structure (Architecture Review Board, Risk Governance, Documentation Governance — Constitution §57-59) is more specific to this platform than any generic Compliance Skill would be |
| Knowledge Graph / Traceability Skill | None found | Not installed — traceability was produced by direct cross-reference verification (`03-TRACEABILITY-MATRIX.md`), which a generic graph-visualization skill would not materially improve for a text-based certification report |
| Decision Analysis Skill | None found beyond `architecture-decision-records` | Not installed — no gap |
| Enterprise Planning Skill | None found | Not installed — no gap; `docs/api-platform/30-ROADMAP.md` already exists and this audit does not re-plan |
| OpenAPI/AsyncAPI-specific validation Skill | None found in the available listing | **Not installed — genuine gap, but not blocking**: `docs/api-platform/17-OPENAPI-GOVERNANCE.md` and `18-ASYNCAPI-EVENTS.md` already specify the standards; an actual OpenAPI linter is a CI-time tool, not a Skill, and its selection is properly deferred to `docs/api-platform/31-ENTERPRISE-PRODUCT-DECISIONS.md`'s existing scope, not re-opened here |

**No new Skill or MCP was installed during this audit.** Every
capability this audit needed (document review, consistency
verification, mechanical link/reference checking, safe-fix application)
was achievable with the existing 9 Skills plus direct Bash/Grep/Python
mechanical checks plus Agent-based research delegation — introducing a
new dependency for a one-time certification pass would not meet the
"meaningful value + actively maintained + no unnecessary complexity"
bar this phase's own instructions set.

## MCP Servers — Status at Audit Time

| Server | Status | Used This Audit? | Reason |
|---|---|---|---|
| `github` | Reconnected mid-session (was briefly disconnected, then reconnected) | No | This audit produces documentation only; no PR/issue/commit-via-API operations were needed — git operations used direct `git`/Bash per this phase's explicit Git Workflow instructions, not the GitHub MCP |
| `bf7c680d-...` (claude-code-remote: routines, triggers, sessions) | Connecting/available | No | No scheduling, cross-session, or trigger capability was needed for a single-pass audit |
| `5d2b3a66-...` | **Requires authentication** — this session is non-interactive and cannot complete an OAuth flow | Not usable | Documented, not silently ignored. **If the user wants this server's capability evaluated, it must be authorized first** — via claude.ai connector settings (if a claude.ai connector) or `claude mcp`/`/mcp` in an interactive session. This Board did not and cannot guess its contents or relevance. |
| `561e560e-...` (generic file-storage connector) | Available | No | Generic cloud file operations (copy/create/download/list/read/search) — not an architecture, audit, or documentation-specific tool |
| `ca4cf8cc-...` (Gmail-like mail connector) | Available | No | Email/label/draft management — not relevant to a repository certification audit |

**Finding: no MCP server was used to generate any certification content.**
Every finding in this document set is traceable to direct repository
reads, mechanical Bash/Python verification, or delegated Agent research
against this repository's own files — never to an external service call.

## Method Note — How This Audit Actually Covered 1,607 Markdown Files

Honest disclosure, consistent with this project's own established
practice of disclosing audit-method scope rather than implying uniform
depth where it wasn't applied (see `docs/reuse/MASTER_COMPARISON_MATRIX.md`'s
own "Scope note" precedent):

1. **Full direct read**: every file in `docs/constitution/` (4),
   `docs/adr/` (12), `docs/architecture-review/` (14),
   `docs/api-platform/` (34), `.claude/context/` (9), plus
   `.claude/SKILLS-INVENTORY.md`, `.claude/SKILLS-VALIDATION-REPORT.md`,
   root `README.md` and `CLAUDE.md` — 74 files read in full this audit
   (in addition to having authored nearly all of them earlier in this
   same session, giving this Board direct, first-hand knowledge of
   their content, not just a fresh read).
2. **Mechanical, exhaustive verification across all 1,607 files**:
   broken-relative-link scan, broken-backtick-file-reference scan,
   TODO/FIXME/placeholder scan — these are deterministic, complete
   scans, not sampling.
3. **Delegated deep-read verification** for the two largest trees
   (`docs/reuse/`, 1,396 files; `docs/discovery/`, 99 files): three
   parallel research passes, each reading every `MASTER_*.md`/top-level
   summary file in full plus a representative spot-check of individual
   module/phase subdirectories, cross-verified against the
   `.claude/context/` ground truth this Board already trusts (itself
   already certified accurate by the completed EARB phase). This is
   the same honest-disclosure discipline this project has applied
   throughout — a full manual re-read of every one of ~1,378 individual
   reuse Feature files would not materially change this audit's
   conclusions beyond what the MASTER summary files plus targeted
   spot-checks already surface, and was not performed.
