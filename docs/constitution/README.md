# Project Constitution — README

## What this is

`PROJECT-CONSTITUTION.md` is the governing rule set for the platform's
architecture: module boundaries, data ownership, tenancy, security,
device integration, AI governance, localization, and the practices
(ADRs, testing, git workflow) that keep the architecture coherent.

It is **not**:
- The Software Architecture Document (SAD) — that comes later and describes
  *how* systems are built to satisfy these rules.
- An implementation plan, roadmap, or task list.
- A final Module Catalog.
- A legal/regulatory compliance certification.

## Authority

The Constitution has precedence over any individual module's local design
choices. See `PROJECT-CONSTITUTION.md` Section 1 (Purpose and Authority) for
the full statement, and Section 45 (Constitution Amendment Process) for how
it may be changed.

## Relationship to other project documents

| Document | Role |
|---|---|
| `CLAUDE.md` | Working-agreement summary for how work is done session-to-session (git workflow, no-guessing rule, etc.). |
| `.claude/context/*.md` | Context Store — Draft/Proposed/Accepted/Rejected/Superseded status-tagged facts, principles, decisions, glossary, open questions. Feeds this Constitution; updated by it when a decision becomes Accepted. |
| `docs/adr/*.md` | Architecture Decision Records — the evidence trail behind every `Accepted` decision referenced in this Constitution. |
| `PROJECT-CONSTITUTION.md` | This document — governing rules. |
| `REVIEW-REPORT.md` | Internal quality review of the Constitution + ADRs + Context for contradictions, gaps, and open risks. |
| Software Architecture Document (future) | Concrete technical design satisfying these rules. Not created in this task. |

## How to propose a change

See `PROJECT-CONSTITUTION.md` Sections 44 (Exception Process) and 45
(Constitution Amendment Process). In short: no silent deviation, no silent
edits to `Accepted` content — every change is either an approved Exception
or a new/superseding ADR plus a `CHANGELOG.md` entry.

## Version

Current version: **v2.1** (Accepted). See `CHANGELOG.md` for history.
