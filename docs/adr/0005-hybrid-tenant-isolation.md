# 0005: Hybrid Tenant Isolation

## Status

Accepted

## Context

The platform is Multi-Tenant, Multi-Organization, Multi-Branch from v1
(vision.md, Constitution Section 18). Tenants will vary widely: some will
be small/medium organizations comfortable with shared infrastructure;
others (large or regulated tenants handling highly sensitive medical data —
`constraints.md` #5) may require stronger, dedicated isolation for
regulatory or contractual reasons. A single fixed isolation strategy must
serve both without over- or under-provisioning isolation for either group.

## Decision

The platform uses **Hybrid Tenant Isolation**: shared infrastructure with
strict logical isolation (every query/command explicitly scoped by Tenant,
enforced server-side) for small and medium tenants, and a dedicated
database or dedicated deployment option for large or regulated tenants.
Tenant isolation must be testable — an automated test suite proves tenant A
can never read/write tenant B's data through any code path, across both
tiers.

## Alternatives Considered

- **Fully shared, logical isolation only (no dedicated option).**
  Rejected: cannot satisfy large/regulated tenants who may have contractual
  or regulatory requirements for stronger isolation (Open Question: local
  legal requirements, `open-questions.md` #2).
- **Dedicated database/deployment per tenant, always.** Rejected as the
  default: operationally expensive and unjustified for small tenants;
  conflicts with "do not over-engineer infrastructure prematurely."
- **Hybrid: shared by default, dedicated as an available option for
  large/regulated tenants.** **Chosen.** Matches the actual variance in
  tenant needs without committing to the most expensive option for every
  tenant.

## Positive Consequences

- Cost-effective default (shared) for the common case, without blocking
  tenants that need stronger isolation.
- A single architectural model accommodates the full tenant range instead
  of a special-cased rewrite when the first large/regulated tenant arrives.

## Negative Consequences

- Two isolation tiers means two things to test, monitor, and operate
  (though the same logical-isolation code path underlies both).
- The exact default data-partitioning technique for the shared tier (e.g.,
  tenant ID column vs. separate schema) is left to the SAD — this ADR does
  not fully specify implementation, which could allow ambiguity if not
  resolved before implementation begins.

## Risks

- **Logical isolation bug** in the shared tier causing cross-tenant data
  leakage. Mitigated by mandatory Multi-Tenant Isolation Testing
  (Constitution Section 36) — a dedicated automated suite attempting
  cross-tenant access and asserting denial, required before any
  tenant-scoped module is done.
- **Unclear promotion path** from shared to dedicated tier for a growing
  tenant. Logged as an implementation detail for the SAD, not resolved
  here.

## Verification

- Automated Multi-Tenant Isolation Testing suite (Constitution Section 36),
  run against both tiers.
- Every tenant-scoped entity has an explicit tenant-identifying
  attribute (schema review checklist, Constitution Section 18).

## Revisit Triggers

- A regulatory requirement (once `open-questions.md` #2 is answered) that
  the two-tier model cannot satisfy for a given market.
- Measured operational cost of the dedicated tier at scale prompting a
  refinement of the promotion/demotion path between tiers.
