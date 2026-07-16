# Diagram — Enterprise Capability Map, Category Level (Wave 3)

**Note:** a 100-node diagram (one per capability) would be unreadable and
decorative, not informative — this shows the 10 categories and their
primary dependency direction instead, which is the genuinely useful
at-a-glance view. Full per-capability detail is in
`artifacts/W3-enterprise-capability-map.md`.

```mermaid
flowchart TB
  Clinical["1. Clinical and Diagnostic (13)<br/>incl. Core Domain proposal"]
  LabOps["2. Laboratory Operations (11)"]
  Workforce["3. Workforce (8)"]
  Financial["4. Financial (11)"]
  Supply["5. Supply Chain (10)"]
  Asset["6. Asset and Device Operations (8)"]
  CustOps["7. Customer Operations (9)"]
  SaaS["8. SaaS and Platform (14)"]
  Governance["9. Governance (8)"]
  Data["10. Data and Intelligence (8)"]

  Clinical --> LabOps
  LabOps --> Supply
  LabOps --> Asset
  Clinical --> Financial
  Financial --> Governance
  Workforce --> Governance
  Supply --> Financial
  CustOps --> Clinical
  SaaS --> Governance
  Data -. reads from all .-> Clinical
  Data -. reads from all .-> LabOps
  Data -. reads from all .-> Financial
  Data -. reads from all .-> Workforce
  Data -. reads from all .-> Supply
  Governance -. governs all .-> Clinical
  Governance -. governs all .-> Financial
  Governance -. governs all .-> Workforce
  Governance -. governs all .-> SaaS
```
