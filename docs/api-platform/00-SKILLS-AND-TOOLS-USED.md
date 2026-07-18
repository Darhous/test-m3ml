# Skills and Tools Used — API Platform & Developer Ecosystem Strategy (Part 1)

Per this phase's mandatory pre-work requirement, every Skill and MCP
capability available in this environment was inspected before any
document in this set was drafted. This file is the honest record of
what was discovered, used, installed, or rejected — nothing is silently
skipped.

## Skills Discovered (full inventory of `.claude/skills/`)

| Skill | Discovered | Used This Phase | Why |
|---|---|---|---|
| `api-design-principles` | ✓ | ✓ | Directly authoritative for REST/HTTP method semantics, versioning strategy options, pagination/error-model best practice — the core reference for `05`, `06`, `07`. |
| `architecture-decision-records` | ✓ | ✓ | Required to correctly read, cite, and reason about ADR status/lifecycle for `15-ADR-REVIEW.md`, and to apply the same rigor already established in the EARB phase. |
| `domain-driven-design` | ✓ | ✓ | Required to classify API types per Module without violating Bounded Context boundaries (`03-API-DOMAIN-INVENTORY.md`), to keep endpoint/resource naming in Ubiquitous Language (`06-NAMING-CONVENTIONS.md`), and to apply the Anti-Corruption Layer pattern consistently at every external-Engine API boundary (`02`, `11`). |
| `stride-analysis-patterns` | ✓ | ✓ | Directly authoritative for the STRIDE threat model required in `11-API-SECURITY.md`. |
| `architecture-patterns` | ✓ | Not invoked | `.claude/skills/architecture-patterns` exists but its subject matter (general architecture pattern catalog) is already superseded for this phase's purposes by the Modular-Monolith/DDD/Bounded-Context discipline already Accepted in ADR-0001/0002/0012 and reapplied via `domain-driven-design`. Invoking it risked re-deriving architecture already frozen, which this phase's Do-Not list forbids. Rejected as redundant, not as low-quality. |
| `c4-architecture` | ✓ | Not invoked | C4 diagramming is a documentation-notation skill for system/container/component diagrams. Part 1 is explicitly scoped to API governance and standards, not diagrams of the platform's containers — no file in the required 15 calls for a C4 diagram. Deferred; likely relevant to the eventual Software Architecture Document, not this phase. |
| `mermaid-diagrams` | ✓ | Not invoked | Considered for illustrating the request/response lifecycle in `02-API-FIRST-ARCHITECTURE.md`. Declined: the lifecycle is fully and unambiguously specified in prose/table form, and this phase's Stop Conditions emphasize governance substance over presentation; adding diagrams was judged as scope creep beyond what the 15 required files ask for, not a quality gap. Available for a future revision if requested. |
| `threat-mitigation-mapping` | ✓ | Not invoked | Overlaps with `stride-analysis-patterns`, which was already sufficient to produce the OWASP API Security Top 10 + STRIDE mapping in `11-API-SECURITY.md`. A dedicated deep mitigation-catalog pass was judged out of scope for Part 1 (Observability, SLA, and detailed incident-response mapping are explicitly reserved for Part 2 / SAD). |
| `doc-coauthoring` | ✓ | Not invoked | A collaborative live-editing workflow skill; not applicable to a single-pass Board-authored deliverable with no separate human co-author in this turn. |

**Skills discovered: 9. Skills used: 4. Skills discovered-but-rejected: 5 (all with documented reason, none rejected for lack of maturity — all are project-local, already vetted skills).**

## MCP Servers Inspected

| Server | Discovered | Relevant to this phase | Disposition |
|---|---|---|---|
| `github` | ✓ | Only for eventual git/PR operations, not architecture content generation | Not used for content; the mission's own Git Workflow (CLAUDE.md Section 16: `git pull --rebase` → commit → `git push origin main`) is followed directly via Bash/git, not via GitHub MCP PR tooling, since no PR was requested. |
| `561e560e-...` (generic file-storage connector) | ✓ | No — generic cloud file storage (copy/create/download/list/read/search files), not an architecture, API-design, or documentation tool | Not used. |
| `ca4cf8cc-...` (Gmail-like mail connector) | ✓ | No — email/label/draft management | Not used. |
| `5d2b3a66-...` | ✓ (listed as requiring authentication) | Unknown — this session cannot authorize it (non-interactive), so its capability could not be inspected | **Documented as a discovered-but-inaccessible capability**, not silently ignored. If the user wants it evaluated for relevance to API Platform work, it must first be authorized via `claude mcp` / `/mcp` in an interactive session — this Board did not and could not guess its contents. |
| `claude-code-remote` (routines/triggers/session tools) | ✓ | No — scheduling/session-orchestration utility, not an architecture tool | Not used. |

**No new Skill or MCP was installed.** No missing capability was found that would have justified a search-and-install per the mandatory pre-work step 4 — every required output (`01`–`15`) was achievable with the existing Skill set plus direct reasoning grounded in `docs/reuse/`, `docs/architecture-review/`, `docs/adr/`, and `.claude/context/`.

## Tasks Automated vs. Completed Manually

- **Automated/Skill-assisted:** REST/HTTP standards baseline (`api-design-principles`), ADR lifecycle correctness and citation discipline (`architecture-decision-records`), Bounded-Context-safe API classification and Ubiquitous-Language-consistent naming (`domain-driven-design`), STRIDE threat enumeration (`stride-analysis-patterns`).
- **Manual (no Skill covers this):** Cross-referencing every one of the 28 Modules against the frozen Technology Baseline (`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`) to classify Internal/External/Partner/Public/Admin/Integration/Future API surface per Module (`03-API-DOMAIN-INVENTORY.md`) — this required direct knowledge of this project's specific `docs/reuse/` and `docs/architecture-review/` content, which no generic Skill encodes. Similarly, the ADR-0011 Accept/Amend recommendation (`15-ADR-REVIEW.md`) required direct, manual reasoning against this project's own Constitution and prior Board findings, not a Skill template.

## Tool Limitations Encountered

- The `domain-driven-design` and `stride-analysis-patterns` Skills are general-purpose reference frameworks, not project-aware — they do not know this platform's specific 28 Modules, ADRs, or frozen Technology Baseline. They informed *method*, not *content*; every concrete classification and recommendation in this document set was derived directly from this project's own artifacts, per the No-Guessing Rule.
- No Skill or MCP could resolve the two genuine capability gaps this phase surfaces honestly rather than papers over: **no API Gateway product and no Secrets/Vault Engine has been evaluated or ratified in the Technology Baseline** (see `10-API-GATEWAY.md` and `12-SECRETS-AND-KEYS.md`). This is a Build-vs-Buy gap, not a tool limitation this session could close — closing it would mean re-opening Technology Baseline evaluation, which this phase's Do-Not list forbids. Both gaps are recorded as new entries in `.claude/context/open-questions.md` (#28, #29) per CLAUDE.md Section 12.
