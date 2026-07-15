# Skills Inventory

Project-scoped skills installed under `.claude/skills/`. All installations copy
only `SKILL.md` + necessary `references/`/`assets/` markdown (and one reference
Python template, see notes) — no scripts, hooks, or commands were copied or
executed. Installation date for all entries below: **2026-07-15**.

---

## 1. doc-coauthoring

- **Purpose**: Structured 3-stage workflow (Context Gathering → Refinement &
  Structure → Reader Testing) for co-authoring documentation, proposals, and
  specs.
- **Source repository**: https://github.com/anthropics/skills
- **Source path**: `skills/doc-coauthoring/`
- **Official or community**: Official (Anthropic)
- **License**: Apache 2.0 (repo-level; this particular skill has no
  standalone LICENSE.txt, unlike `docx`/`pdf`)
- **Commit hash**: `9d2f1ae187231d8199c64b5b762e1bdf2244733d`
- **Installation directory**: `.claude/skills/doc-coauthoring/`
- **Files copied**: `SKILL.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none
- **Security notes**: Pure workflow/instruction text. No shell, network, or
  file-system side effects.
- **Trigger examples**: "write documentation", "draft a proposal/spec",
  "help me co-author this doc"
- **Update procedure**: Re-fetch `skills/doc-coauthoring/SKILL.md` from the
  same repo/commit range and diff before replacing.
- **Removal procedure**: `rm -rf .claude/skills/doc-coauthoring`

## 2. architecture-patterns

- **Purpose**: Clean Architecture, Hexagonal Architecture, and DDD-flavored
  backend architecture patterns; layering, dependency direction, bounded
  context refactors.
- **Source repository**: https://github.com/wshobson/agents
- **Source path**: `plugins/backend-development/skills/architecture-patterns/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `b6af3711058190e4b5c5274b9758498fe626ec5a`
- **Installation directory**: `.claude/skills/architecture-patterns/`
- **Files copied**: `SKILL.md`, `references/advanced-patterns.md`,
  `references/details.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none
- **Security notes**: Reviewed for shell commands, secrets, prompt-injection
  phrasing — clean. Contains example code (e.g. Stripe `api_key` variable
  name) that is illustrative only, not a real credential.
- **Trigger examples**: "design clean architecture for X", "refactor this
  monolith into bounded contexts", "hexagonal vs layered architecture"
- **Update procedure**: Re-fetch from same repo path; MIT license allows
  free redistribution/modification.
- **Removal procedure**: `rm -rf .claude/skills/architecture-patterns`

## 3. architecture-decision-records

- **Purpose**: Writing and maintaining ADRs for technical decisions.
- **Source repository**: https://github.com/wshobson/agents
- **Source path**: `plugins/documentation-generation/skills/architecture-decision-records/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `b6af3711058190e4b5c5274b9758498fe626ec5a`
- **Installation directory**: `.claude/skills/architecture-decision-records/`
- **Files copied**: `SKILL.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none
- **Security notes**: Clean — instruction-only content.
- **Trigger examples**: "document this decision", "write an ADR for X",
  "why did we choose Y over Z"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/architecture-decision-records`

## 4. api-design-principles

- **Purpose**: REST/GraphQL API design and review standards.
- **Source repository**: https://github.com/wshobson/agents
- **Source path**: `plugins/backend-development/skills/api-design-principles/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `b6af3711058190e4b5c5274b9758498fe626ec5a`
- **Installation directory**: `.claude/skills/api-design-principles/`
- **Files copied**: `SKILL.md`, `references/details.md`,
  `references/graphql-schema-design.md`, `references/rest-best-practices.md`,
  `assets/api-design-checklist.md`, `assets/rest-api-template.py`
- **Scripts included**: `assets/rest-api-template.py` — **not an executable
  script**, a static FastAPI reference/example file the skill points to for
  illustration (mock in-memory data, no real DB/network calls). Copied as a
  reference template per installation rule 6; **never executed**.
- **Scripts excluded**: none beyond the above
- **Dependencies**: none required to use the skill itself; the reference
  template mentions `fastapi`/`pydantic`/`uvicorn` only as illustrative
  imports, not installed.
- **Security notes**: Reviewed line-by-line for `curl|wget|sudo|eval|exec|
  os.system|subprocess` patterns — clean. Mentions of "password"/"token"/
  "api_key" are field/parameter names in example schemas, not real secrets.
- **Trigger examples**: "design a REST API for X", "review these endpoints",
  "GraphQL schema for Y"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/api-design-principles`

## 5. stride-analysis-patterns

- **Purpose**: STRIDE-based threat identification for systems/features.
- **Source repository**: https://github.com/wshobson/agents
- **Source path**: `plugins/security-scanning/skills/stride-analysis-patterns/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `b6af3711058190e4b5c5274b9758498fe626ec5a`
- **Installation directory**: `.claude/skills/stride-analysis-patterns/`
- **Files copied**: `SKILL.md`, `references/details.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none
- **Security notes**: Clean — analytical/instructional content only.
- **Trigger examples**: "run a STRIDE analysis on X", "threat model this
  login flow"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/stride-analysis-patterns`

## 6. threat-mitigation-mapping

- **Purpose**: Maps identified threats to concrete mitigations/controls.
- **Source repository**: https://github.com/wshobson/agents
- **Source path**: `plugins/security-scanning/skills/threat-mitigation-mapping/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `b6af3711058190e4b5c5274b9758498fe626ec5a`
- **Installation directory**: `.claude/skills/threat-mitigation-mapping/`
- **Files copied**: `SKILL.md`, `references/details.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none
- **Security notes**: Clean.
- **Trigger examples**: "map these threats to mitigations", "prioritize
  security remediations for X"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/threat-mitigation-mapping`

## 7. c4-architecture

- **Purpose**: Generates C4 model (Context/Container/Component/Deployment)
  documentation using Mermaid syntax.
- **Source repository**: https://github.com/softaworks/agent-toolkit
- **Source path**: `skills/c4-architecture/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `3027f20f3181758385a1bb8c022d4041dfb4de84`
- **Installation directory**: `.claude/skills/c4-architecture/`
- **Files copied**: `SKILL.md`, `README.md`, `references/advanced-patterns.md`,
  `references/c4-syntax.md`, `references/common-mistakes.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none)
- **Dependencies**: none — output is Mermaid text, rendered by whatever
  Markdown viewer the user already uses.
- **Security notes**: Reference/syntax documentation only. Clean.
- **Trigger examples**: "create a C4 context diagram for X", "document
  system architecture with C4"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/c4-architecture`

## 8. mermaid-diagrams

- **Purpose**: General-purpose Mermaid diagram generation (sequence, class,
  ER, flowcharts, state, C4, etc.) and troubleshooting.
- **Source repository**: https://github.com/softaworks/agent-toolkit
- **Source path**: `skills/mermaid-diagrams/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `3027f20f3181758385a1bb8c022d4041dfb4de84`
- **Installation directory**: `.claude/skills/mermaid-diagrams/`
- **Files copied**: `SKILL.md`, `README.md`, `references/advanced-features.md`,
  `references/architecture-diagrams.md`, `references/c4-diagrams.md`,
  `references/class-diagrams.md`, `references/erd-diagrams.md`,
  `references/flowcharts.md`, `references/sequence-diagrams.md`
- **Scripts included**: none
- **Scripts excluded**: none (skill has none). Note: `SKILL.md` mentions an
  *optional* `npm install -g @mermaid-js/mermaid-cli` for local PNG/SVG
  rendering — this was **not run** and is not required to use the skill
  (Mermaid renders natively in Claude Code/most Markdown viewers).
- **Dependencies**: none required; optional external CLI mentioned above is
  not installed.
- **Security notes**: Reference documentation only. Clean.
- **Trigger examples**: "diagram this login flow", "sequence diagram for X",
  "visualize this database schema"
- **Update procedure**: Re-fetch from same repo path.
- **Removal procedure**: `rm -rf .claude/skills/mermaid-diagrams`

## 9. domain-driven-design

- **Purpose**: Strategic DDD (bounded contexts, context mapping, ubiquitous
  language, subdomain classification) and tactical DDD (aggregates, entities,
  value objects, repositories, domain events). Explicitly supports Modular
  Monolith and warns against premature microservice extraction.
- **Source repository**: https://github.com/wondelai/skills
- **Source path**: `domain-driven-design/`
- **Official or community**: Community
- **License**: MIT
- **Commit hash**: `326b3801223ad277ae7082ff85435ba1d36e1903`
- **Installation directory**: `.claude/skills/domain-driven-design/`
- **Files copied**: `SKILL.md`, `references/bounded-contexts.md`,
  `references/building-blocks.md`, `references/domain-events.md`,
  `references/repositories-factories.md`, `references/strategic-design.md`,
  `references/ubiquitous-language.md`
- **Scripts included**: none
- **Scripts excluded**: repo-level `scripts/generate-codex-plugins.sh` exists
  at the root of `wondelai/skills` but belongs to the repo's own build
  tooling, not to this skill folder — it was never fetched or copied.
- **Dependencies**: none
- **Security notes**: Reviewed for shell/network/prompt-injection patterns —
  clean. Content is conceptual/pattern-focused.
- **Trigger examples**: "define bounded contexts for X", "how do we split
  this big system", "aggregate design for Y", "ubiquitous language for Z"
- **Update procedure**: Re-fetch from same repo path (sparse-checkout on
  `domain-driven-design/` only to avoid pulling the other 50+ unrelated
  skills in this repo).
- **Removal procedure**: `rm -rf .claude/skills/domain-driven-design`

---

## Deferred Skills (approved in scope, not installed yet)

| Skill | Reason for deferral |
|---|---|
| `skill-creator` | Not needed before there is an actual need to build a custom skill. |
| `docx` | Reserved for the final export stage only. |
| `pdf` | Reserved for the final export stage only; will avoid dependencies that require `sudo` (e.g. `poppler-utils` for OCR) when eventually installed. |
| `microservices-patterns` | Deferred to avoid biasing early design toward microservices; initial direction is Modular Monolith with gradual extraction if justified. |

See `SKILLS-VALIDATION-REPORT.md` for the full DDD-skill search process and
rejected alternatives.
