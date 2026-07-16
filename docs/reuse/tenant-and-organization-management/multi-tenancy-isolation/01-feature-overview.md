# Feature: Multi-Tenancy Isolation

**Module:** Tenant and Organization Management (Platform Kernel)
**Source (Discovery):** ADR 0005 (Hybrid Tenant Isolation, Accepted —
model is Shared-tier + Dedicated-tier); Constitution Section 18/19
(Multi-Tenant Isolation, Tenant Isolation Testing); `open-questions.md`
#15 (the exact shared-tier partitioning technique — tenant-ID-column vs.
schema-per-tenant — still Open); Risk Register #17/SEC-04 (**Highest**
severity — cross-tenant data leakage, directly caused by #15 being Open).

## What This Feature Covers

The concrete technical mechanism for the **shared tier** of ADR 0005's
already-Accepted Hybrid model: how one shared database serves many
tenants without one tenant ever reading another's data. This is not a
new architectural decision (ADR 0005 already settled Shared vs. Dedicated
at the model level) — it is the missing technical-mechanism layer
`open-questions.md` #15 explicitly defers to "the Software Architecture
Document later." This Feature's research is offered as evidence toward
that future decision, **not** a resolution of #15 itself — resolving a
Discovery-tracked Open Question is outside this program's mandate (this
program does Build-vs-Buy/Reuse research, not architectural decisions).
