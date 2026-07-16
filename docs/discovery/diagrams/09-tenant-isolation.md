# Diagram — Tenant Isolation, Applied to Real Bounded Contexts (Phase 09)

```mermaid
flowchart LR
  subgraph Shared["Shared Infrastructure (small/medium tenants)"]
    T1[Tenant: Organization A]
    T2[Tenant: Organization B]
    subgraph SharedModules["Per-Module Schemas (ADR 0003)"]
      OM_S[(Order Management Schema)]
      SM_S[(Specimen Management Schema)]
      TP_S[(Test Processing Schema)]
      BC_S[(Billing and Claims Schema)]
    end
    T1 -.tenant-scoped rows, category TBD.-> OM_S
    T2 -.tenant-scoped rows, category TBD.-> OM_S
  end
  subgraph Dedicated["Dedicated (large/regulated tenants)"]
    T3[Tenant: Organization C]
    subgraph DedicatedModules["Per-Module Schemas, Dedicated DB"]
      OM_D[(Order Management Schema)]
      SM_D[(Specimen Management Schema)]
      TP_D[(Test Processing Schema)]
      BC_D[(Billing and Claims Schema)]
    end
    T3 --> OM_D
  end
```

**Note:** this diagram makes explicit what the Constitution's own
illustrative Section 19 diagram left abstract — tenant partitioning
(horizontal, per-tenant) and Schema per Module (ADR 0003, per-module) are
two independent axes that apply *together*, not as alternatives.
