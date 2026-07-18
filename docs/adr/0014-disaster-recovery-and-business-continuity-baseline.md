# 0014: Disaster Recovery and Business Continuity Baseline

## Status

**Accepted (Pre-SAD Baseline Correction, 2026-07-18).**

## Context

`23-SAD-READINESS-MATRIX.md` (Architecture Readiness Review,
2026-07-18) identified Disaster Recovery as the repository's one
genuine "Missing Inputs" section — no prior phase (Constitution,
Discovery, Reuse Intelligence, Technology Baseline, API Platform)
addressed backup strategy, recovery objectives, or DR topology at any
depth. Constitution §34 (Reliability and Resilience Rules) and R-08
(vendor exit-strategy risk, `docs/architecture-review/11-RISKS.md`)
are adjacent but not equivalent to a DR baseline.

**This ADR establishes architecture principles and a classification
framework — it does not invent final commercial SLAs.** Per the
No-Guessing Rule (CLAUDE.md §3), no specific RPO, RTO, availability
percentage, retention period, or regional topology is asserted as
Decided here unless it is already supported by existing repository
evidence (none is, for numeric targets specifically). Every numeric
placeholder below is explicitly labeled **Proposed Target**, **Pending
Business Approval**, **Pending Regulatory Validation**, or **Pending
Workload Evidence** — never presented as approved.

## Decision

**A four-tier Service Criticality classification, backup/recovery
principles, and DR governance process are Accepted as the platform's
Disaster Recovery and Business Continuity architecture baseline.**
Final numeric RPO/RTO targets per tier are **not** Accepted by this ADR
— they are structurally tracked, pending the inputs named below.

## Service Criticality Tiers

| Tier | Definition | Representative Modules (illustrative, not exhaustive) |
|---|---|---|
| **Tier 1 — Life/Safety or Clinically Critical** | Data or function whose unavailability or loss directly risks patient safety or clinical decision integrity | Result Verification and Reporting (`TestResult`, `ResultVerified`, `ResultReleased`), Diagnostic Ordering, Specimen Operations, Patient Management |
| **Tier 2 — Core Operational** | Data or function required for the platform's primary revenue-generating and day-to-day operational workflows, not itself life/safety-critical | Scheduling and Encounters, Laboratory Execution, Billing, Insurance and Corporate Contracts, Identity and Access |
| **Tier 3 — Business Support** | Data or function supporting the business but tolerant of longer recovery windows without directly halting clinical or revenue operations | Workforce Management, Payroll, Procurement, Supplier Management, Accounting, CRM and Support |
| **Tier 4 — Non-Critical Analytics/Auxiliary** | Derived, recomputable, or non-authoritative data; loss is inconvenient, not operationally blocking | Analytics (Superset dashboards), non-authoritative reporting caches, AI Operations Gateway request logs (not the audit trail itself) |

**Tier assignment is per-Module, performed at SAD/Implementation time**
using this table's definitions — this ADR fixes the classification
framework and 4 tiers, not the exhaustive per-Module assignment (a SAD
responsibility, informed by this framework).

## Recovery Classes and Numeric Targets (Structured, Not Final)

| Tier | RPO | RTO | Status |
|---|---|---|---|
| Tier 1 — Life/Safety/Clinical | *[to be set]* | *[to be set]* | **Proposed Target: near-zero RPO, shortest RTO of any tier** — exact figures Pending Business Approval and Pending Regulatory Validation (Egypt health-authority requirements, tied to Open Question #2/#25's existing Legal Dependency status) |
| Tier 2 — Core Operational | *[to be set]* | *[to be set]* | **Proposed Target: low RPO/RTO, materially looser than Tier 1** — Pending Business Approval and Pending Workload Evidence (real transaction-volume data, same dependency already tracked for capacity assumptions, D-54) |
| Tier 3 — Business Support | *[to be set]* | *[to be set]* | **Proposed Target: moderate RPO/RTO** — Pending Business Approval |
| Tier 4 — Non-Critical Analytics/Auxiliary | *[to be set]* | *[to be set]* | **Proposed Target: best-effort, longest RTO of any tier, RPO may exceed 24h** — Pending Business Approval |

**No cell in this table is Accepted as a final number by this ADR.**
The table's purpose is to make the *dependency* trackable and
assignable — exactly the structure this phase's mandate requires
("Provide a structured table that allows final RPO and RTO to be
approved later per service criticality tier") — not to assert values
this repository has no evidence for.

## Backup Principles (Accepted)

- Every Tier 1 and Tier 2 data store has an automated, scheduled backup
  process — no manual-only backup procedure is acceptable for these
  tiers.
- Backups are encrypted at rest, consistent with the platform's general
  Data Protection posture (Constitution §29-30).
- Backups are access-controlled independently from the production data
  store's own access-control list — a compromised production credential
  must not automatically grant backup access.
- **Immutable or protected backup storage is required for Tier 1 and
  Tier 2** — a backup must not be modifiable or deletable through the
  same credential/path that could compromise the live system (ransomware
  and insider-threat resilience), consistent with the Full Auditability
  and tamper-evidence discipline already established for the audit
  trail (immudb, E4).

## Restore Verification (Accepted)

- A backup is not considered valid until a restore has been
  successfully tested against it — an unverified backup is treated as
  equivalent to no backup for Tier 1 and Tier 2.
- DR testing cadence (how often restores are verified) is **Pending
  Business Approval** — no specific frequency is asserted here.

## Geographic and Failure-Domain Principles (Accepted)

- Tier 1 and Tier 2 backups are stored in a failure domain independent
  of the primary production environment (a separate availability zone
  at minimum) — a single-zone failure must not be able to destroy both
  the primary data and its backup simultaneously.
- Cross-region replication/backup storage is **Pending Regulatory
  Validation** — this is directly entangled with the already-tracked
  Egypt cross-border data transfer Legal Dependency (Open Question #25,
  R-13); this ADR does not resolve that dependency, it inherits it.
- Consistent with ADR-0009 (SaaS First, On-Premise Ready, Hybrid
  Ready), DR topology must remain deployable across SaaS, On-Premise,
  and Hybrid modes — a DR design that only works in one deployment mode
  is not acceptable.

## Tenant Data Recovery Considerations (Accepted)

- DR recovery must respect Hybrid Tenant Isolation (ADR-0005) — a
  recovery operation for one Tenant's Dedicated-tier deployment must
  not require access to, or risk exposure of, another Tenant's data,
  whether Shared- or Dedicated-tier.
- Per-Tenant selective recovery (restoring one Tenant's data without a
  full-environment restore) is a **Proposed Target** capability for the
  Dedicated tier specifically — not yet a confirmed requirement for the
  Shared tier, where RLS-based co-location (ADR-0013, D-42) makes
  selective single-Tenant restore architecturally harder and is
  explicitly **Pending Workload Evidence** on whether it is actually
  needed.

## Encryption and Access-Control Requirements (Accepted)

Restates, does not duplicate, requirements already established
elsewhere: backups inherit the platform's existing encryption-at-rest
posture (Constitution §29) and are access-controlled via the same
Policy-Based Access model (ADR-0008/OPA) used for production data —
DR infrastructure is not a lower-security side channel.

## Dependency Recovery Responsibilities (Accepted)

**Updated 2026-07-18 (Final Pre-SAD Semantic Consistency Correction):**
the rule below replaces an earlier version of this section that named a
specific Engine count (21) — a number that was already stale relative
to the Technology Baseline's own count at the time and, more
fundamentally, does not belong in a durable architectural rule. The
rule now stated is deliberately count-independent.

- **Every ratified Engine or stateful platform component that stores
  authoritative data, recoverable configuration, secrets, policies,
  integration state, or operational metadata must have an explicitly
  assigned backup, restore, recovery-validation, and disaster-recovery
  responsibility.** This applies uniformly across however many Engines
  the Technology Baseline ratifies at any point in time — the rule does
  not require updating when the Baseline's count changes.
- Ownership belongs to the responsible **Module, Bounded Context,
  Independent Component, platform capability, or operational owner**,
  as recorded in the Technology Baseline's Owner column
  (`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`), the SAD,
  deployment documentation, or a dedicated ownership register — whichever
  is authoritative for that component. Not every Engine's Single
  Adoption Point maps to a conventional domain Module; some are owned by
  a platform capability (e.g., a shared Identity or Observability
  capability) rather than a Bounded Context.
- Not every stateless library or Reference Standard requires an
  independent backup strategy in its own right. However, the
  configuration, secrets, policy definitions, schemas, and
  infrastructure definitions that operate a component may still require
  recovery even when the runtime component itself is otherwise
  stateless — statelessness of the runtime does not imply nothing about
  it needs to be recoverable.
- Central platform operations may coordinate DR execution across
  Engines and components (e.g., a shared backup schedule or a common
  restore-drill calendar), but responsibility for each Engine's or
  component's actual recovery must remain **explicitly assigned** —
  coordination must never collapse into an undifferentiated central
  obligation that no single owner is accountable for.
- This is the natural extension of R-08 (No formal vendor exit strategy
  documented) — an Engine's exit strategy and its DR/backup strategy
  are related but distinct deliverables; this ADR does not merge them,
  and R-08 remains open and separately tracked.

## Disaster Declaration and Recovery Governance (Accepted)

- A "disaster" is formally declared through the Architecture Review
  Board's existing governance apparatus (Constitution §57) — no ad hoc
  or informal declaration path is architecturally sanctioned.
- Recovery execution is logged as an Audit Event (Full Auditability,
  Accepted Architecture Principle #10) — a disaster recovery operation
  is itself a Sensitive Operation for audit purposes, consistent with
  the treatment already given to Break-Glass Access (ADR-0008).

## DR Testing Expectations (Accepted, Frequency Not Fixed)

- DR capability must be periodically tested (restore verification
  above), not assumed to work based on backup completion alone.
- Specific testing cadence and scope (tabletop exercise vs. full
  failover drill) are **Pending Business Approval** — not asserted
  here.

## Relationship Between SaaS, On-Premise, and Hybrid Deployment Modes

- **SaaS (Shared tier)**: this platform's own operational team owns DR
  execution end-to-end.
- **On-Premise**: the Tenant's own infrastructure team shares DR
  responsibility per a documented split — the exact split is a
  commercial/contractual matter (Legal Dependency), not resolved here.
- **Hybrid**: DR responsibility follows whichever tier (Shared or
  Dedicated) actually holds the data for that Tenant, consistent with
  ADR-0005's existing Hybrid Tenant Isolation model.

## Consequences

### Positive

- Closes `23-SAD-READINESS-MATRIX.md`'s one "Missing Inputs" finding —
  the SAD now inherits a governed framework rather than a blank
  section.
- Establishes tier-based prioritization before any numeric commitment
  is made, avoiding the failure mode of committing a platform-wide RTO
  number that is either unrealistically strict for Tier 4 or
  unacceptably loose for Tier 1.
- Makes every numeric dependency explicitly trackable (the table above)
  rather than an undifferentiated "DR is TBD" statement.

### Negative

- The SAD still cannot state final RPO/RTO commitments — this ADR
  converts an undefined gap into a well-structured, still-open
  dependency, not a closed one. This is an honest limitation, not a
  design flaw: the missing inputs (business risk appetite, regulatory
  findings, real workload data) still do not exist anywhere in this
  repository.

## Constraints

- No Module or SAD section may assert a specific RPO/RTO/availability
  number citing this ADR as its source — this ADR provides
  classification and process, not final targets.
- Tier 1 classification decisions require Architecture Review Board
  sign-off, not unilateral Module-team assignment, given the
  clinical-safety stakes involved.

## Alternatives Considered

- **Defer DR entirely to Implementation, no ADR now.** Rejected: this
  phase's explicit mandate requires that "the absence of final
  business-approved numbers must not remain a missing SAD input after
  this phase" — a structured, numerically-incomplete framework
  satisfies that requirement; complete silence would not.
- **Assert a single platform-wide RPO/RTO number now.** Rejected:
  would either be fabricated (violating the No-Guessing Rule) or
  arbitrarily conservative/loose without tier differentiation, both
  worse outcomes than a labeled, trackable placeholder structure.
- **Merge DR scope into R-08 (Exit Strategy risk).** Rejected: exit
  strategy (replacing a vendor Engine) and disaster recovery
  (restoring after a failure) are related but distinct concerns with
  different triggers, owners, and testing regimes — conflating them
  would weaken both.

## Reversibility and Exit Strategy

Reversible via a superseding ADR through Constitution Section 45, as
with every ADR in this repository. The tier classification framework
is expected to be *refined* (numeric targets added) rather than
*reversed* — refinement (adding numbers once evidence exists) does not
require a superseding ADR, only an amendment recording the newly
approved figures against this ADR's existing table structure.

## Verification Requirements

- The SAD's Disaster Recovery section cites this ADR and populates the
  Recovery Classes table's per-Tier RPO/RTO cells only once the
  labeled dependency (Business Approval / Regulatory Validation /
  Workload Evidence) is actually satisfied — never speculatively.
- Every Module's Tier assignment (Tier 1-4) is recorded at SAD time and
  is itself traceable to this ADR's classification definitions.
