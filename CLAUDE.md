# Project Instructions

## 1. Project Description (brief)

A digital healthcare platform. Starting point: laboratory management. Long-term
goal: a broad, extensible healthcare platform with a central backend, a unified
login, and role/permission/data-scope/organization/branch-based routing to the
right Portal/Dashboard. Not a plain CRUD system.

## 2. Context

Before any architecture-related work, read `.claude/context/`:
`README.md`, `vision.md`, `architecture-principles.md`, `decisions.md`,
`glossary.md`, `module-catalog.md`, `open-questions.md`, `constraints.md`,
`stakeholders.md`.

## 3. No-Guessing Rule

Do not invent requirements, modules, tech choices, or numbers that are not in
`.claude/context/` or explicitly stated by the user. If something is unknown,
add it to `open-questions.md` instead of assuming an answer.

## 4. Read Context First

Read the relevant `.claude/context/` files before proposing or changing
anything architectural. Do not re-derive context that already exists there.

## 5. Use ADRs for Big Decisions

Any significant architectural decision must go through the
`architecture-decision-records` skill and produce an ADR before it is treated
as `Accepted` in `decisions.md`.

## 6. No Forced Microservices

Do not default to a microservices design. Microservices are an option to
justify later, not a starting assumption.

## 7. Modular Monolith First

The initial architectural direction is Modular Monolith with clear Bounded
Contexts, extractable into services later only when justified.

## 8. Respect Module Boundaries

Modules must not depend on another module's internal implementation details.
Prefer explicit contracts/events over shared internals.

## 9. No Code Without an Explicit Request

Do not write product code unless the user explicitly asks for it in that
turn.

## 10. No Final Documents Before Requirements Are Settled

Do not produce a final Software Architecture Document or Project
Constitution before requirements are reasonably settled (see
`open-questions.md`).

## 11. Separate Facts, Assumptions, Recommendations, Decisions

When discussing architecture, label statements clearly as one of: Fact,
Assumption, Recommendation, or Decision. Do not blend them.

## 12. Keep Context Files Current

When a new decision, term, or open question emerges, update
`decisions.md`, `glossary.md`, and `open-questions.md` accordingly.

## 13. No Real Medical or Personal Data

Never use real medical data or real personal data in examples, tests, or
diagrams. Use fictitious/anonymized sample data only.

## 14. Backend-Enforced Security

Authorization and access control must be enforced in the backend, not only
in the UI.

## 15. Human-in-the-Loop for Medical AI

AI must never issue a final, unreviewed medical decision. Sensitive
AI-assisted actions require human review.

## 16. Git Workflow

- All completed work stages are saved on `main`.
- Before starting work: `git pull --rebase origin main`.
- After each completed stage: a clear commit, then `git push origin main`.
- Force push is forbidden.
- On conflict or a rejected push: stop and ask the user — do not guess a resolution.

---

This file is a working-agreement summary, not an architecture document.
