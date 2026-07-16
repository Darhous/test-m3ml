# Diagrams — Candidate Aggregates (Phase 05)

## Subdomain 1 — Order Management

```mermaid
classDiagram
  class TestOrder {
    OrderID
    Status
  }
  class OrderedTestList {
    TestCatalogRefs
  }
  class OrderingActorRef {
    ActorID
    ActorType
  }
  class TestCatalogEntry {
    TestCode
  }
  class SpecimenRequirement {
    Description
  }

  TestOrder --> OrderedTestList
  TestOrder --> OrderingActorRef
  TestCatalogEntry --> SpecimenRequirement
  OrderedTestList ..> TestCatalogEntry : references by ID
```

## Subdomain 2 — Specimen Management

```mermaid
classDiagram
  class Specimen {
    SpecimenID
    Status
  }
  class CollectionDetails {
    CollectedBy
    CollectedAt
    Location
  }
  class RejectionReason {
    ReasonCode
    Note
  }
  class ChainOfCustodyRecord {
    HandoffLog
  }

  Specimen --> CollectionDetails
  Specimen --> RejectionReason
  Specimen --> ChainOfCustodyRecord
  Specimen ..> TestOrder : references by ID
```

## Subdomain 3 — Test Processing and Result Verification (Core)

```mermaid
classDiagram
  class TestResult {
    ResultID
    Status
  }
  class ResultValue {
    Measurement
    Unit
    ReferenceRange
  }
  class VerificationRecord {
    VerifiedBy
    VerifiedAt
  }
  class ProvenanceInfo {
    Source
    DeviceRef
    RawPayloadRef
  }

  TestResult --> ResultValue
  TestResult --> VerificationRecord
  TestResult --> ProvenanceInfo
  TestResult ..> Specimen : references by ID
  TestResult ..> TestOrder : references by ID
```

## Subdomain 5 — Billing and Claims

```mermaid
classDiagram
  class Invoice {
    InvoiceID
    Status
  }
  class LineItem {
    Description
    Amount
  }
  class Claim {
    ClaimID
    Status
  }

  Invoice --> LineItem
  Invoice ..> Claim : references by ID
  Claim ..> Invoice : references by ID
```
