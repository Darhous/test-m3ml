# Discovery — README

## Status

**Framework only. Discovery has not been executed.** This directory
currently contains the *methodology* for running Discovery
(`DISCOVERY-FRAMEWORK.md`, `EXECUTION-GUIDE.md`, `EXECUTE-DISCOVERY.md`, and
12 playbooks under `prompts/`), not any actual business/domain findings.
`artifacts/`, `reports/`, and `diagrams/` are currently empty (each has its
own placeholder README explaining what will populate it once Discovery
runs).

## What This Directory Is

An Enterprise Discovery Framework for the digital healthcare platform
project (`darhous/test-m3ml`, starting point Laboratory Management),
designed to run entirely underneath the already-Accepted
`docs/constitution/PROJECT-CONSTITUTION.md` v2 and its 10 ADRs
(`docs/adr/0001`–`0010`). It exists to make Discovery a controlled,
auditable, single-responsibility-per-step process instead of an unstructured
conversation, and to produce the Discovery Book that a future Software
Architecture Document task will consume — Discovery does not itself produce
that SAD, and this framework does not execute Discovery on its own.

## Directory Structure

```
docs/discovery/
├── README.md                    — this file
├── DISCOVERY-FRAMEWORK.md       — the WHAT/WHY: phases, dependencies,
│                                   produce/consume matrix, where Context/
│                                   ADRs get updated, quality gates,
│                                   Definition of Complete
├── EXECUTION-GUIDE.md           — the HOW: running the framework session-
│                                   to-session, stop/review/commit points,
│                                   resuming, handling Open Questions/
│                                   Assumptions/Conflicts
├── EXECUTE-DISCOVERY.md         — the compact operational run-script a
│                                   future single prompt follows to invoke
│                                   Playbooks 02–12 in sequence
│
├── prompts/                     — the 12 reusable playbooks (methodology
│   ├── 01_MASTER.md               layer + a short "Project Bindings"
│   ├── 02_BUSINESS_DISCOVERY.md   section per file — see
│   ├── 03_EVENT_STORMING.md       DISCOVERY-FRAMEWORK.md Section 2,
│   ├── 04_DOMAIN_DISCOVERY.md     "Reuse Design")
│   ├── 05_DOMAIN_MODELING.md
│   ├── 06_BOUNDED_CONTEXTS.md
│   ├── 07_BUSINESS_RULES.md
│   ├── 08_INTEGRATIONS.md
│   ├── 09_SAAS_PLATFORM.md
│   ├── 10_AI_DISCOVERY.md
│   ├── 11_VALIDATION.md
│   └── 12_FINAL_DISCOVERY_BOOK.md
│
├── artifacts/                   — structured working outputs per phase
│                                   (maps, catalogs, candidate models,
│                                   the execution ledger) — currently empty
├── reports/                     — per-phase and cross-phase narrative
│                                   reports (findings, open items,
│                                   conflicts raised/resolved) — currently
│                                   empty
└── diagrams/                    — Mermaid/C4 diagrams produced by each
                                    phase — currently empty
```

**Why `artifacts/`, `reports/`, and `diagrams/` are separated from
`prompts/`:** the `prompts/` folder is designed to be copyable, close to
as-is, into a future Enterprise project as a reusable Discovery
methodology. `artifacts/`, `reports/`, and `diagrams/` are this project's
specific Discovery *outputs* and are not reusable — keeping them in
separate folders means the reusable core never gets tangled with
project-specific content (see `DISCOVERY-FRAMEWORK.md` Section 2).

## How to Use This Directory

1. Read `DISCOVERY-FRAMEWORK.md` first — understand the phase order,
   dependencies, and what each phase produces/consumes.
2. Read `EXECUTION-GUIDE.md` — understand the operating discipline (stop
   points, review points, git checkpoints, how Open Questions/Assumptions/
   Conflicts are handled).
3. When actually running Discovery (a future task, not this one), follow
   `EXECUTE-DISCOVERY.md` as the literal step-by-step script, which in turn
   invokes each playbook under `prompts/` in order.

## What This Directory Is Not

- Not the Software Architecture Document (SAD) — Discovery's output is an
  *input* to a future SAD task, never a replacement for it.
- Not a place where Business Domains, Events, or Architecture get decided
  as part of building this framework — this framework was built without
  executing any of its own playbooks (per the explicit instruction that
  created it).
- Not a final Module Catalog — `.claude/context/module-catalog.md` remains
  governed by its own existing rule (categories only, no final list) even
  after Discovery runs; Discovery produces strong *candidates*, per
  Constitution Section 2/46.
- Not a place to select a programming language, framework, cloud provider,
  database product, message broker, or AI provider — this restriction
  applies to the framework itself and to everything it will later produce.

## Relationship to Other Project Documents

| Document | Role relative to this framework |
|---|---|
| `CLAUDE.md` | Working-agreement rules (No-Guessing, git workflow) this framework operates under, not around. |
| `docs/constitution/PROJECT-CONSTITUTION.md` | The governing rules Discovery must never contradict; every playbook cites the specific sections it depends on. |
| `docs/adr/*.md` | The 10 Accepted decisions Discovery narrows and implements, never reopens without an explicit user-driven Exception/Amendment. |
| `.claude/context/*.md` | The Context Store Discovery reads from and appends to — history always preserved, `Accepted` status only ever written in Playbook 12. |
| Future Software Architecture Document | Consumes this framework's eventual output (the Discovery Book); not started by this framework. |
