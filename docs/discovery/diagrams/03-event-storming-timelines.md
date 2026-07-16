# Diagrams — Event Storming Timelines (Phase 03)

## VS1 — Walk-in Test Order to Verified Result Delivery

```mermaid
sequenceDiagram
    participant Doctor
    participant Patient
    participant Lab as Laboratory Staff
    participant Device as Lab Analyzer Device
    participant Sys as System

    Doctor->>Lab: Order Test
    Lab-->>Lab: TestOrdered
    Patient->>Lab: arrives, specimen collected
    Lab-->>Lab: SpecimenCollected
    Lab-->>Lab: SpecimenAccessioned
    Lab-->>Lab: SpecimenQualityChecked (pass)
    Lab->>Device: Start Processing
    Device-->>Lab: TestResultCaptured
    Lab-->>Lab: ResultVerified (Pivotal)
    Lab-->>Sys: Release Result
    Sys-->>Sys: ResultReleased (Pivotal)
    Sys->>Patient: PatientNotified
    Sys->>Doctor: DoctorNotified
```

## VS2 — Home Sample Collection

```mermaid
sequenceDiagram
    participant Patient
    participant Sup as Support Staff
    participant Coll as Sample Collector
    participant Lab as Laboratory Staff

    Patient->>Sup: HomeVisitRequested
    Sup-->>Sup: HomeVisitScheduled
    Sup->>Coll: CollectorDispatched
    Coll->>Patient: visits
    Coll-->>Coll: SpecimenCollectedAtHome
    Coll->>Lab: SpecimenTransportedToLab
    Lab-->>Lab: SpecimenAccessioned (converges with VS1)
```

## VS3 — Specimen Rejected and Recollected

```mermaid
sequenceDiagram
    participant Lab as Laboratory Staff
    participant Sys as System
    participant Patient
    participant Doctor

    Lab-->>Lab: SpecimenQualityChecked (fail)
    Lab-->>Lab: SpecimenRejected (Pivotal)
    Sys->>Patient: PatientNotifiedOfRejection
    Sys->>Doctor: DoctorNotifiedOfRejection
    Patient->>Lab: RecollectionScheduled
    Note over Lab: Re-enters VS1/VS2 at Collection
```

## VS4 — Insurance Claim Billing Cycle

```mermaid
sequenceDiagram
    participant Sys as System
    participant Fin as Finance Staff
    participant Payer as Insurance/Payer System
    participant Patient

    Sys-->>Sys: BillableEventIdentified (from ResultReleased)
    Sys-->>Fin: InvoiceGenerated
    Fin->>Payer: InsuranceEligibilityChecked
    Fin->>Payer: ClaimSubmitted
    Payer-->>Fin: ClaimAdjudicated (Pivotal, external-originated)
    Fin->>Patient: PatientBalanceSettled
```
