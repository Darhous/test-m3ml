# Expanded Persona Catalog (Wave 2)

**Status: Draft — mixed provenance.** Roles/categories below are
`Confirmed` (the user's authorization prompt names them explicitly). Each
persona's Goals/Pain Points/Decisions/KPIs are `Inferred — Industry
Reference` unless noted — same discipline as the Baseline Discovery's
Persona Catalog (`artifacts/12-persona-catalog.md`, retained, extended
here rather than replaced). Two role names in the user's list are
organization types, not personas (**Clinics**, **Hospitals**) — represented
here via their actual human actors (Clinic Administrator, Hospital
Administrator/Medical Director) with a note, not dropped silently.

## Clinical and Care Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Patient *(retained from Baseline, unchanged)* | Trustworthy fast result, clear cost | Unclear rejection reasons, opaque billing | Own records only | None (read/request only) | Time-to-result |
| Guardian | Act on behalf of a dependent (minor, elderly) safely | Unclear delegated-access process | Dependent's records, via Consent (Constitution Section 22) | Consent grant/revoke | Consent accuracy |
| Referring Doctor *(retained)* | Fast reliable results, order on patient's behalf | Delayed results, unclear escalation | Own patients' records | Order placement | Turnaround time |
| Consultant / Specialist | Deep clinical history access for referred cases | Fragmented history across facilities | Referred-patient records only | Clinical interpretation input | Referral resolution time |
| Clinic Administrator *(represents "Clinics" in the user's list)* | Smooth daily clinic operation, scheduling efficiency | Manual scheduling conflicts | Clinic-branch scope | Staff/schedule changes | Appointment utilization |
| Hospital Administrator / Medical Director *(represents "Hospitals")* | Institution-wide clinical + operational oversight | Cross-department visibility gaps | Organization-wide scope | Policy configuration (verification rules, Wave 6) | Institutional compliance rate |

## Laboratory Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Laboratory Staff (Technician) *(retained)* | Clear worklists, accurate tracking | Unclear verification eligibility (Open Q #19) | Branch-scoped specimens/results | Specimen processing | Rejection rate |
| Medical Director | Clinical governance across the lab | Balancing throughput vs. safety | Organization-wide | Verification policy sign-off | Safety incident rate |
| Pathologist / Result Verifier *(retained, refined)* | Unambiguous authority to verify | Eligibility criteria still Open (#19) | Assigned test-type scope | `ResultVerified`, `ResultCorrected` (Sensitive Operations) | Verification accuracy |
| Quality Staff | Maintain accreditation posture | Manual audit trail assembly | Organization-wide QC data | CAPA initiation | Non-conformance closure rate |

## Front-Office and Support Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Reception | Fast, accurate patient intake | Duplicate patient records | Branch-scoped | Patient record creation | Intake time |
| Call Center Agent | Resolve inquiries without escalation | No unified view of patient/order status | Read-mostly, cross-branch (per policy) | None (advisory) | First-contact resolution |
| Customer Support | Resolve complaints, coordinate fixes | Cross-domain visibility (billing + clinical + logistics) | Case-scoped, cross-domain read | Complaint resolution actions | Complaint resolution time |

## Financial Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Cashier | Accurate point-of-sale collection | Manual reconciliation at shift end | Branch-scoped transactions | Payment recording, refund initiation | Cash variance |
| Accountant | Accurate books, audit-ready ledger | Manual journal entry from disparate sources | Organization-wide financial data | Journal entries, reconciliation | Close-cycle time |
| Finance Manager | Revenue/cost visibility, control | Delayed consolidated reporting | Organization-wide, cross-branch | Pricing/discount policy approval | Margin accuracy |

## Workforce Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| HR Staff | Accurate employee records, compliant processes | Manual credential-expiry tracking | Organization-wide HR data | Employee record changes | Data accuracy |
| Payroll Staff | Accurate, on-time, confidential payroll | Payroll-data privacy exposure risk (flagged, Wave 12) | Strictly scoped — payroll data is among the most sensitive non-clinical data in the platform | Payroll run execution | Payroll accuracy/timeliness |

## Supply Chain Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Procurement Staff | Timely, cost-effective purchasing | Manual supplier evaluation | Organization-wide procurement data | Purchase order approval | Cost savings |
| Inventory Staff | Accurate stock, no stockouts/expiry waste | Manual expiry/lot tracking | Branch/warehouse-scoped | Stock adjustments | Stockout rate, waste rate |
| Store/Warehouse Manager | Efficient stock flow across branches | Cross-branch transfer visibility | Multi-branch, org-scoped | Stock transfer approval | Transfer cycle time |
| Supplier *(external)* | Predictable orders, timely payment | Opaque order status | Own orders only (via Partner/API pattern) | None (external, read-mostly via portal) | Order fulfillment rate |
| Courier / Home Visit Staff *(retained, refined)* | Clear routes, successful visits | No-show handling (Open Q #22) | Assigned visit scope only | Specimen chain-of-custody handoff | Visit success rate |

## Commercial and External Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Insurance User (Payer-side contact) | Accurate, fast claims processing | Manual eligibility verification | Claim-scoped only | Adjudication decisions (external system, Constitution Section 24-pattern ACL) | Claim turnaround |
| Corporate Client (Contract Owner) | Predictable, contract-compliant billing | Lack of self-service reporting | Own organization's aggregate data | Contract terms negotiation (offline) | Contract compliance rate |
| Partner / API Client *(external)* | Stable integration contract | Breaking changes without notice | Own integration scope only | API key management | Integration uptime |

## Technical and Platform Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Device Engineer | Reliable device connectivity | Diagnosing intermittent device failures | Device/branch-scoped diagnostic data | Device configuration | Device uptime |
| Integration Engineer | Stable, well-documented contracts | Ambiguous contract versioning | Integration-scoped | Contract/schema changes | Integration error rate |
| Platform Operator | Platform-wide health and configuration | Cross-tenant operational visibility need vs. isolation requirement (tension, flagged Wave 12) | **Platform-wide — highest-privilege persona in the model**, must be Least-Privilege-scoped per Constitution Section 21 | Cross-tenant configuration, Break-Glass access | Platform uptime |
| Tenant Administrator | Manage own tenant's org/branch/user setup | Feature entitlement confusion | Tenant-wide | User/role provisioning | Tenant health |
| Branch Administrator | Manage own branch's daily operations | Cross-branch policy inconsistency | Branch-scoped | Branch-local configuration | Branch operational KPI |

## Governance and External Oversight Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| Auditor *(internal or external)* | Complete, tamper-evident audit trail | Manual evidence assembly | Read-only, audit-scoped (Constitution Section 23) | None (read-only by design) | Audit completeness |
| Compliance Staff | Defensible regulatory posture | Egypt-specific requirements still `Requires Legal Verification` (Wave 11) | Organization-wide compliance data | Policy configuration | Compliance incident rate |
| Legal Reviewer *(external, human-in-the-loop for legal, not AI)* | Confirm regulatory claims before they're made | No structured hand-off point from Discovery | Read access to Legal Verification Register (Wave 11) | Legal sign-off | N/A — advisory role |
| Regulator *(external, not a platform user in the normal sense)* | Institutional compliance visibility (if/when required) | Not yet designed — Open | Not yet designed | N/A | N/A |

## Commercial Operations Personas

| Persona | Goals | Key Pain Points | Data Scope | High-Risk Actions | Primary KPI |
|---|---|---|---|---|---|
| SaaS Commercial Team | Manage plans, subscriptions, entitlements | Manual entitlement changes | Cross-tenant commercial data (own company's SaaS operator role, not a tenant's data) | Plan/entitlement changes | Churn rate, expansion revenue |
| Support Operations | Platform-wide support triage | Cross-tenant visibility need vs. isolation (same tension as Platform Operator) | Case-scoped, elevated when authorized | Elevated access grants | Support SLA adherence |
| AI Operations | Monitor AI Gateway health/quality | No dedicated persona existed in Baseline Discovery | AI action audit trail (Constitution Section 23/28) | AI model/prompt configuration (never clinical decision authority) | AI suggestion acceptance rate |

## Summary

**39 personas identified** (37 human/organizational + 2 external
non-human-operated: Partner/API Client and Regulator, both still
represented by a human point of contact). Compared to the Baseline
Discovery's 4 detailed personas (Patient, Doctor, Laboratory Staff,
Laboratory Management) plus 11 table-only stakeholder categories, this is
a **~3x expansion** in named personas and the first time Financial,
Workforce, Supply Chain, Platform/SaaS, and Governance personas exist
anywhere in this project's Discovery output.
