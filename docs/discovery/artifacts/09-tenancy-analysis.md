# Tenancy Analysis (Discovery, Phase 09)

**Status: Draft — Assumption-Driven Autonomous Run.** Does not re-litigate
Hybrid Tenant Isolation (ADR 0005) — narrows its open implementation
details only (Constitution Section 46 items 15–16), per this playbook's
explicit Constitution binding.

## Per-Context Tenant-Scope Confirmation

| Bounded Context | Aggregate(s) | Tenant Identifier Present? | Finding |
|---|---|---|---|
| Order Management | TestOrder, TestCatalogEntry | **Gap** | Phase 05's candidate structure did not explicitly model Tenant/Organization/Branch fields on `TestOrder`. Constitution Section 18 requires an explicit identifier, not an implied one — flagged for the future SAD to add explicitly, not assumed present. `TestCatalogEntry` may be Organization-level shared reference data rather than per-Tenant — flagged as a design question, not resolved here. |
| Specimen Management | Specimen | **Gap** | Same finding — `Specimen` references `TestOrder` by ID; whether it also needs its own denormalized Tenant/Branch reference (for query/isolation efficiency) is an SAD-level decision, but the *requirement* that it be scoped is confirmed by Constitution Section 18 regardless of the mechanism. |
| Test Processing and Result Verification | TestResult | **Gap** | Same finding — and the highest-stakes one, since `TestResult` carries the most sensitive data of any Aggregate in the model. |
| Billing and Claims | Invoice, Claim | **Gap**, plus a Localization gap | Same Tenant-scope finding. Additionally: `LineItem`'s `Amount` field (Phase 05) was modeled as a raw value with no currency — **Localization Gap**, see below. |
| Notification and Communication | NotificationRequest | **Gap** | Same Tenant-scope finding, lower stakes (Generic Subdomain). |
| Device and Equipment Integration | DeviceImportRecord | **Gap**, plus a Localization gap | Same Tenant-scope finding. Additionally: device timestamps need explicit timezone handling distinct from platform-recorded timestamps (device clock vs. platform clock may differ) — **Localization Gap**, see below. |
| Core Platform (both) | (Organization, Branch, User, Role, Permission, Policy) | **N/A — these concepts ARE the tenancy/scoping mechanism** | Already governed at Constitution level (Section 18/21); not a gap, this is the scoping infrastructure itself. |

**Overall finding:** every business Aggregate from Phase 05 needs an
explicit Tenant-scoping mechanism added before implementation — none of
Phase 05's candidate structures included one, because Phase 05 was
tactical-modeling-focused and tenancy is a cross-cutting concern layered on
afterward. This is normal DDD sequencing, not an error, but it must not be
silently forgotten heading into the SAD.

## Localization Gaps (Constitution Section 32)

| Aggregate | Field | Gap | Proposed Refinement (Design proposal, not a requirement confirmation) |
|---|---|---|---|
| Invoice / LineItem | `Amount` | No currency attached | Model as a `Money` Value Object: `{amount, currencyCode}`, not a raw number — satisfies Constitution Section 32's "no hardcoded currency" rule. |
| DeviceImportRecord | `timestamp` | No timezone context | Model as `{deviceTimestamp, deviceTimezoneRef, platformReceivedTimestamp}` — preserves both the device's local time and an unambiguous platform-side reference, relevant to Multi-Branch operation across timezones. |
| TestOrder / Specimen / TestResult | (all timestamp fields, implicit) | Not explicitly modeled with timezone context in Phase 05 | Same principle applies platform-wide — flagged here once as a pattern, not repeated per Aggregate. |

## Narrowing `open-questions.md` #15 (Shared-Tier Data-Partitioning Technique)

**Two viable categories identified** (consistent with ADR 0005, no
database product named):

1. **Tenant-identifier-column category**: every tenant-scoped table carries
   an explicit Tenant reference column; logical isolation enforced by
   mandatory query scoping + database permission checks (Constitution
   Section 19's own "strict logical isolation" language).
2. **Schema-per-tenant-within-shared-database category**: each tenant gets
   a dedicated schema inside the same physical database.

**Important clarification (not previously stated explicitly):** this
choice is a *separate axis* from Schema per Module (ADR 0003) — Schema per
Module partitions by **owning Module** (Order Management schema vs.
Specimen Management schema, etc.); tenant partitioning is an *orthogonal*
concern *within* each module's own schema. Category 1 could be applied
inside each module's schema without conflicting with ADR 0003 at all;
Category 2 would mean each module's schema is itself further subdivided
per tenant, which is a heavier structural choice. **Neither is chosen
here** — both are handed to the SAD as viable candidates, per this
playbook's explicit "not fixed here" scope boundary.

## Narrowing `open-questions.md` #16 (Tier-Promotion Path)

**Trigger type proposed** (evidence-based, no arbitrary threshold, per
Constitution Section 55's Evolution Strategy discipline): a tenant is
considered for promotion from the shared tier to the dedicated tier when
either (a) measured, sustained resource consumption data shows shared-tier
isolation is operationally strained for that tenant, or (b) the tenant has
a contractual/regulatory requirement the shared tier's logical isolation
cannot satisfy (per ADR 0005's own Revisit Triggers language). **No
specific metric/number is proposed** — that would require real operational
data this session does not have.

## `open-questions.md` #3 (Hosting Model Detail) and #4 (Expected Scale)

**No new evidence available this session for either.** Both remain fully
Open — this phase does not narrow them, and does not invent placeholder
figures. Stated explicitly per the No-Guessing Rule rather than silently
skipped.

## ADR Revisit Trigger Check

Checked every finding above against ADR 0005 (Hybrid Tenant Isolation),
ADR 0009 (SaaS First/On-Premise/Hybrid Ready), ADR 0010 (Localization
First) Revisit Triggers sections — **no finding in this phase fires any of
them.** The Localization Gaps found are implementation-completeness gaps
within the already-Accepted ADR 0010 commitment, not evidence the
commitment itself needs revisiting.
