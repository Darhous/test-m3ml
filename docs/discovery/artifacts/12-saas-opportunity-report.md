# SaaS Opportunity Report (Discovery, Phase 12)

**Status: Draft — Assumption-Driven Autonomous Run.** Synthesized from
Phase 09's tenancy findings and the already-Accepted ADR 0005/0009. Not new
business-strategy content — candidate opportunities *implied* by the
already-Accepted architecture posture, flagged for real business
validation, not proposed as confirmed strategy.

## Candidate Opportunities (Inferred, pending business validation)

| Opportunity | Basis | Confidence |
|---|---|---|
| Tiered offering (shared vs. dedicated infrastructure) as a product packaging axis, not just a technical one | ADR 0005 (Hybrid Tenant Isolation) already Accepted at the architecture level — a natural product-tier mapping (Standard vs. Enterprise/Regulated) is implied, not yet a confirmed pricing/packaging decision | Medium |
| Multi-branch/multi-organization expansion within a single Tenant as a natural upsell path | `vision.md`'s Confirmed Organization/Branch model already supports this structurally | Medium |
| On-Premise/Hybrid deployment as a differentiator for regulated/enterprise healthcare customers specifically | ADR 0009 already Accepted; Discovery adds no new evidence, only notes the opportunity follows directly from an existing decision | Medium |
| Home Collection Logistics (Specimen Management) as a distinct convenience-led market position | Directly tied to the unresolved Core Domain alternative (ADR 0011's "Why Proposed" section) — if real business strategy confirms this angle, it simultaneously answers the Core Domain question and identifies a go-to-market opportunity | Low-Medium — speculative until the Core Domain question is genuinely resolved |
| Arabic/English + RTL support as a regional differentiator | ADR 0010 already Accepted; Discovery notes the market opportunity this decision was presumably made to capture, without inventing specific target markets (`open-questions.md` #1 remains Open) | Low — no real market data exists to substantiate this beyond the ADR's own stated rationale |

## Explicit Non-Claims

This report does **not** claim any of these opportunities are validated,
prioritized, or committed — it exists so a future business-strategy
conversation has a documented starting list drawn from what the
architecture already supports, rather than starting blank. None of these
should be read into the Software Architecture Document as a requirement.
