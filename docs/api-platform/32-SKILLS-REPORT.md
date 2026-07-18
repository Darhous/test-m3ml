# Skills and Tools Used — Part 2

Companion to `00-SKILLS-AND-TOOLS-USED.md` (Part 1). This report covers
only what changed or was newly exercised in Part 2 — it does not
repeat Part 1's inventory verbatim.

## Skills Discovered (re-verified, unchanged inventory)

`.claude/skills/` was re-listed at the start of this phase; the
inventory is identical to Part 1's 9 Skills. No new Skill appeared, no
Skill was removed.

## Skills Used This Phase

| Skill | Used | Why (Part 2-specific) |
|---|---|---|
| `architecture-patterns` | ✓ (newly invoked this phase) | Clean/Hexagonal Architecture's Ports-and-Adapters framing directly informed `16-CONTRACT-FIRST.md`'s "contract as port, implementation as adapter" framing, and its explicit Anti-Corruption Layer / Shared Kernel guidance grounded `16`'s Schema Governance rule (when a DTO may vs. may not be shared across Module contracts). Not invoked in Part 1 because Part 1 had no contract-sharing design decision to make. |
| `mermaid-diagrams` | ✓ (newly invoked this phase) | Part 2's subject matter (webhook delivery sequences, contract-testing pipelines, system contexts for the Developer Portal and Marketplace) is materially more diagram-shaped than Part 1's governance-and-standards content was. Diagrams appear in `16`, `18`, `19`, `22`, `24`. |
| `c4-architecture` | ✓ (newly invoked this phase) | Used specifically for the Developer Portal (`22`) and Marketplace (`24`) System Context diagrams — both are new architectural roles this phase introduces, and C4 Context is the appropriate, lightest-weight level for introducing a new system's boundary and actors without over-specifying its internals (which remain implementation, out of scope). |
| `threat-mitigation-mapping` | ✓ (newly invoked this phase) | Informed `19-WEBHOOKS.md`'s Security section (SSRF validation at subscription registration, signing-secret rotation with grace period) as defense-in-depth layering applied to a channel `11-API-SECURITY.md`'s STRIDE model did not originally cover (outbound delivery to an uncontrolled external endpoint). |
| `domain-driven-design` | ✓ (reused from Part 1) | Continued to ground naming and boundary discipline — e.g., `16`'s Shared Kernel caution, `18`'s Domain-Event-vs-Integration-Event distinction. |
| `api-design-principles` | ✓ (reused from Part 1) | Continued to ground REST/versioning references cited throughout `20`, `21`. |
| `architecture-decision-records` | ✓ (reused from Part 1) | No new ADR review was required this phase (Part 2's mission does not include an ADR-Review document), but the lifecycle discipline it establishes was reused for `29-LIFECYCLE.md`'s release-channel framing. |

## Skills Discovered But Not Used (unchanged from Part 1)

`doc-coauthoring` — same reasoning as Part 1: no live human co-authoring
workflow in this turn. `stride-analysis-patterns` was not separately
re-invoked this phase (its Part 1 output remained sufficient and was
extended, not repeated, by `threat-mitigation-mapping`'s layering
guidance).

## MCPs Used

**None**, same finding as Part 1. The `github` MCP remains reserved for
git/PR operations outside this phase's content-generation work; the
generic file-storage and mail connectors remain irrelevant; the
authentication-gated connector (`5d2b3a66-...`) remains inaccessible in
this non-interactive session and is again documented, not silently
dropped.

## New Installations

**None.** No missing capability was found that justified installing a
new Skill or MCP — every required output was achievable with the
existing Skill set.

## Automation Performed

- Diagram generation (`mermaid-diagrams`, `c4-architecture`) for every
  sequence/context diagram embedded in `16`, `18`, `19`, `22`, `24`.
- Cross-document dependency tracing (manual, no Skill covers this): each
  of the 18 documents explicitly cites which other Part 1/Part 2
  document it extends versus duplicates, verified by direct read-back
  of each referenced document's actual content before citing it — this
  is the mechanism that produced the Exit Condition "No duplicated
  architecture" rather than merely asserting it.

## Tasks Completed Manually

- The `31-ENTERPRISE-PRODUCT-DECISIONS.md` evidence assessment for all
  7 categories — no Skill or MCP performs vendor evaluation; this
  required direct reasoning against this project's own established
  evaluation criteria (license family, self-hosting per ADR-0009,
  localization per ADR-0010) applied to general engineering knowledge
  about each candidate category, with an explicit, honest split between
  the 3 categories where that reasoning was sufficient and the 4 where
  it was not.
- Updating `.claude/context/open-questions.md` with items #30–#31 per
  CLAUDE.md Section 12 (Part 1 already added #28–#29).

## Limitations Encountered

- No Skill or MCP has access to real vendor licensing terms beyond
  this Board's own general knowledge as of its training — the HashiCorp
  Vault BUSL license-change fact cited in `31` is stated as background
  knowledge, not verified via a live source in this session (no
  WebFetch/WebSearch was used, consistent with this phase's Do-Not list
  against repeating Build-vs-Buy market research). Any product
  recommendation in `31` should be re-verified against current license
  terms at implementation time, exactly as `02-TECHNOLOGY-BASELINE.md`
  already requires for every ratified Engine.
- As in Part 1, the general-purpose Skills used here (`architecture-
  patterns`, `mermaid-diagrams`, `c4-architecture`, `threat-mitigation-
  mapping`) are not project-aware — every concrete claim about this
  platform's own Modules, ADRs, or Technology Baseline in this document
  set was derived from this project's own artifacts, with the Skills
  informing method and notation only.
