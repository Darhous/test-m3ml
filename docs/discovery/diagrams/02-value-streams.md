# Diagrams — Value Streams (Phase 02)

## VS1 — Walk-in Test Order to Verified Result Delivery

```mermaid
journey
  title VS1: Walk-in Test Order to Verified Result
  section Order
    Doctor orders test: 5: Doctor
    Patient arrives at branch: 4: Patient
  section Collection
    Specimen collected: 4: Laboratory Staff
    Specimen accessioned: 4: Laboratory Staff
  section Processing
    Test processed: 5: Laboratory Staff
    Result captured: 5: Laboratory Staff
  section Release
    Result verified: 5: Laboratory Staff
    Result released: 5: Laboratory Staff
    Patient and doctor notified: 4: Patient, Doctor
```

## VS2 — Home Sample Collection to Verified Result Delivery

```mermaid
flowchart LR
  A[Order and home-visit request captured] --> B[Visit scheduled]
  B --> C[Collector dispatched]
  C --> D[Specimen collected in the field]
  D --> E[Specimen transported and accessioned]
  E --> F[Converges with VS1 from Accessioning onward]
```

## VS3 — Specimen Rejected and Recollected

```mermaid
flowchart LR
  A[Specimen received] --> B{QC check}
  B -->|Pass| C[Continues in VS1/VS2]
  B -->|Fail| D[Specimen rejected with reason code]
  D --> E[Patient and doctor notified]
  E --> F[Recollection scheduled]
  F --> A2[Re-enters VS1/VS2 at Collection]
```

## VS4 — Insurance Claim Billing Cycle

```mermaid
flowchart LR
  A[Billable event identified] --> B[Invoice generated]
  B --> C[Insurance eligibility and coverage determined]
  C --> D{Insurance applicable}
  D -->|Yes| E[Claim submitted]
  E --> F[Claim adjudicated]
  F --> G[Patient balance settled]
  D -->|No| G
```
