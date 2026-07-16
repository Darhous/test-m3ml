# Diagram — Enterprise Context Map, Tiered by Maturity (Wave 9)

```mermaid
flowchart TB
  subgraph Platform["Platform (universal dependency, 3)"]
    IDA[Identity and Access]
    TOM[Tenant and Org Management]
    AC[Audit and Compliance]
  end

  subgraph Modeled["Modeled — Evidenced (9)"]
    PM[Patient Management]
    DO[Diagnostic Ordering]
    SO[Specimen Operations]
    LE[Laboratory Execution]
    RVR[Result Verification and Reporting - Core]
    DI[Device Integration]
    NC[Notification and Communication]
  end

  subgraph Recognized["Recognized — Inferred, Not Yet Deeply Modeled (16)"]
    PCM[Practitioner and Clinic Mgmt]
    SE[Scheduling and Encounters]
    QM[Quality Management]
    AM[Asset and Maintenance]
    INV[Inventory]
    PROC[Procurement]
    SUP[Supplier Management]
    BILL[Billing]
    PT[Payments and Treasury]
    ICC[Insurance and Corporate Contracts]
    ACC[Accounting]
    WM[Workforce Management]
    PAY[Payroll]
    CRM[CRM and Support]
    DOC[Document Management]
    AN[Analytics]
    AI[AI Operations]
    SC[SaaS Commercial Operations]
  end

  RVR --> LE --> SO --> DO
  RVR -. ACL .-> DI
  Modeled --> Platform
  Recognized --> Platform
  AN -. reads all, writes none .-> Modeled
  AN -. reads all, writes none .-> Recognized
  AI -. governed advisory .-> Modeled
  AI -. governed advisory .-> Recognized
```

**Note:** intra-tier edges within "Recognized" are omitted from this
diagram for readability (a full 16-node mesh would be decorative, not
useful) — see `artifacts/W9-bounded-context-remapping.md`'s Context
Mapping table for the specific relationships that matter.
