# Ubiquitous Language Expansion (Wave 8)

**Status: Draft.** Disambiguates the 37 conflict-prone terms the user
named, each pinned to its owning Bounded Context(s) so the same English
word used in two different contexts is never silently assumed to mean the
same thing (the DDD failure mode Constitution Section 6 and the
`domain-driven-design` skill both warn against most strongly: "different
bounded contexts may use the same word with different meanings — and that
is fine," *provided* it's made explicit, which is this table's entire job).

| Canonical Term | AR | Definition (per owning context) | Owning Context(s) | Disambiguation / Forbidden Conflation |
|---|---|---|---|---|
| Order | طلب | A request for a diagnostic test (`TestOrder`, Order Management) | Order Management | **Forbidden:** conflating with "Purchase Order" (Procurement) — the platform has two distinct "Order" concepts; always qualify as "Test Order" or "Purchase Order" in cross-domain text. |
| Request | طلب/استدعاء | Generic term — **forbidden as a standalone domain term**; always qualify (Purchase Request, Home Visit Request, Leave Request) | Cross-cutting | Never use bare "Request" as an Aggregate/Event name — Wave 5's events already correctly qualify every instance (`PurchaseRequested`, `HomeVisitRequested`, `LeaveRequested`). |
| Booking | حجز | **Not used** — this platform uses "Appointment" (Scheduling and Encounters), not "Booking," to match Wave 5's event naming (`AppointmentBooked` uses Booking only as a verb, not a noun) | Scheduling and Encounters | Forbidden as a noun/Aggregate name — use Appointment. |
| Appointment | موعد | A scheduled time slot for a patient-practitioner interaction | Scheduling and Encounters | Distinct from Encounter (below) — an Appointment is the *plan*; an Encounter is the *actual occurrence*. |
| Visit | زيارة | Ambiguous — used informally for both "Home Visit" (Specimen Management) and a walk-in "Encounter" (Clinical) | Specimen Management (Home Visit) / Clinical (Encounter) | **Forbidden** as a bare term — always qualify "Home Visit" explicitly; never use "Visit" alone for a walk-in Encounter. |
| Encounter | زيارة سريرية | The actual occurrence of a patient-practitioner clinical interaction | Patient Management / Scheduling and Encounters | Distinct from Appointment (the plan) — an Encounter may occur without a prior Appointment (walk-in). |
| Sample | عيّنة | **Not used as canonical** — see Specimen | — | Forbidden as a synonym for Specimen in formal artifacts (informal/spoken use only) — Wave 5/Baseline consistently use "Specimen." |
| Specimen | عيّنة | The physical biological material collected from a patient (canonical term, matches Baseline `Specimen` Aggregate) | Specimen Management | Canonical over "Sample" — "Sample" may appear in device/vendor terminology (external, not renamed) but never in platform-owned artifacts. |
| Test | فحص | A specific diagnostic procedure a patient can be ordered for (`TestCatalogEntry`) | Order Management / Laboratory Execution | Distinct from "Analysis" (below) — a Test is the *catalog item ordered*; Analysis is the *act of analyzing*. |
| Analysis | تحليل | The analytical act performed on a Specimen during Test Processing | Laboratory Execution | Not interchangeable with "Test" — "run the Analysis" (verb-like, process), "order the Test" (noun, catalog item). |
| Result | نتيجة | The clinical output of Test Processing (`TestResult` Aggregate) | Test Processing and Result Verification | Canonical; "Finding" or "Value" are **forbidden synonyms** in formal artifacts (both appeared informally in Wave 6's `ResultValue` Value Object — that name is correct as a *field*, not a competing term for the Result concept itself). |
| Report | تقرير | **Two distinct meanings, both retained, always qualified:** (a) Clinical Report — the patient/doctor-facing result document (Clinical context); (b) BI/Enterprise Report — cross-domain analytics output (Analytics context) | Test Processing and Result Verification (a) / Analytics (b) | **Flagged in Wave 3 already** — this Wave formalizes the required qualification: always say "Clinical Report" or "BI Report," never bare "Report" in cross-domain artifacts. |
| Verification | اعتماد | The Sensitive-Operation act of clinically approving a Result (`ResultVerified`) | Test Processing and Result Verification | Canonical, matches Baseline exactly — not to be confused with "Approval" (below), which is a broader cross-domain concept. |
| Approval | موافقة | Generic cross-domain concept — a decision gate (PO Approval, Leave Approval, Expense Approval) distinct from clinical Verification | Cross-cutting (Procurement, Workforce, Financial) | **Forbidden:** using "Approval" for a clinical Result sign-off — that is always "Verification," never "Approval," to keep the Sensitive-Operation term unambiguous. |
| Publication | نشر/إتاحة | **Not used as canonical** — see "Release" (`ResultReleased`, Baseline) | — | Forbidden synonym — "Publication" does not appear in any Baseline or Wave 5 event; "Release" is canonical. |
| Invoice | فاتورة | A billing document for a payable amount (`Invoice` Aggregate) | Billing | Distinct from Receipt (below) — an Invoice requests payment; a Receipt confirms it. |
| Receipt | إيصال | Proof of a completed Payment | Billing / Payments and Treasury | Not currently a modeled Aggregate (gap) — flagged for Wave 9/future SAD; conceptually distinct from Invoice as above. |
| Collection | تحصيل/جمع | **Two distinct meanings, always qualified:** (a) Specimen Collection (Specimen Management); (b) Payment Collection (Financial, "Collections" capability, Wave 3) | Specimen Management (a) / Billing (b) | Never use bare "Collection" across domain boundaries — always qualify. |
| Payment | دفعة/سداد | Settlement of an amount owed (`PatientBalanceSettled`, and general Payments capability) | Payments and Treasury | Canonical. |
| Expense | مصروف | An organizational outgoing cost (`ExpenseRecorded`, Wave 5) | Accounting | Distinct from Payment — an Expense is the platform's own cost; Payment (above) is typically inbound from a patient/customer (though Payments and Treasury also handles outbound supplier payments — flagged as needing further disambiguation in a future SAD). |
| Reagent | كاشف | A consumable chemical used in Test Processing | Inventory / Laboratory Execution | Distinct from generic "Consumable" (below) — a Reagent is a specific, test-linked consumable category. |
| Consumable | مستهلكات | Generic term for any consumable stock item (reagents, collection materials, PPE) | Inventory | Reagent is a *subtype* of Consumable, not a synonym. |
| Lot | دفعة إنتاج | A specific production batch of a Reagent/Consumable from a supplier, with its own expiry | Inventory | Distinct from "Batch" (below) in this platform's usage — see next row. |
| Batch | دفعة معالجة | **Forbidden as a synonym for Lot** in this platform — reserved (if ever needed) for a *processing* batch (e.g., a batch of specimens processed together), not a *supply* batch | Laboratory Execution (if used) | Flagged: this distinction is a Discovery-level naming decision (Recommended), not yet exercised by any real event — no `Batch`-named event exists yet. |
| Tenant | مستأجر | The top-level Multi-Tenant entity (Constitution Section 18, Accepted) | Core Platform | Canonical, Accepted — unchanged. |
| Organization | مؤسسة | An entity operating within a Tenant (Constitution Section 18, Accepted) | Core Platform | Canonical, Accepted — unchanged. |
| Branch | فرع | A location within an Organization (Constitution Section 18, Accepted) | Core Platform | Canonical, Accepted — unchanged. |
| Facility | منشأة | **Not used as canonical** — the user's Business Scope list uses "Clinic and Facility Operations"; this platform's canonical term remains "Branch" or "Organization" depending on level | Core Platform | Forbidden as a fourth competing term — always resolve "Facility" to either Organization or Branch in formal artifacts. |
| Department | قسم | A sub-branch organizational unit (e.g., a hospital department) — **not yet modeled** | *(gap — not yet a Bounded Context concept)* | Flagged as a possible finer-grained unit below Branch, needed once Hospital customer type (Wave 1) is modeled in depth — not resolved here. |
| Employee | موظف | Any staff member in Workforce Management, regardless of clinical role | Workforce Management | Distinct from Practitioner (below) — every Practitioner who is platform staff is also an Employee, but not every Employee is a Practitioner (e.g., Cashier). |
| Practitioner | ممارس صحي | A clinically-licensed role (Doctor, Consultant, Pathologist) — see Wave 2 Personas | Practitioner and Clinic Management | Superset of "Doctor" — every Doctor is a Practitioner, but Practitioner also covers Consultants/Pathologists. |
| Doctor | طبيب | A specific Practitioner sub-type who orders tests/treats patients | Practitioner and Clinic Management | Canonical, matches Baseline's "Referring Doctor" persona. |
| Patient | مريض | The recipient of clinical care (Wave 5 Cluster G, now an owned domain) | Patient Management | Canonical, matches Baseline. |
| Guardian | ولي أمر | A person with Consent-based delegated authority over a Patient (Wave 2) | Patient Management | Distinct from Patient — never conflate; a Guardian acts *on behalf of*, never *as*, a Patient. |
| Subscriber | مشترك | **Not used as canonical for a person** — reserved for a Tenant's subscription relationship (SaaS Commercial) | SaaS Commercial Operations | Forbidden as a synonym for Patient/Customer — "Subscriber" always refers to the Tenant-level commercial relationship. |
| Customer | عميل | Ambiguous across two levels, always qualified: (a) the Patient as a service recipient (informal); (b) the Tenant/Corporate Client as the SaaS/commercial customer | Patient Management (a, informal only) / SaaS Commercial (b) | **Forbidden** as a bare formal term — always say "Patient" for (a) or "Tenant"/"Corporate Client" for (b). |
| Partner | شريك | An external API client or business partner (Wave 1/2) | Partner and Marketplace Operations | Canonical, matches Wave 1/2 usage. |

## Summary

**37 terms disambiguated**, closing every collision the user explicitly
flagged. 6 terms (Booking, Sample, Publication, Facility, Subscriber, and
bare "Customer"/"Request"/"Collection"/"Visit") are **forbidden** as
standalone canonical terms — each has a designated canonical replacement.
1 genuine gap surfaced (Department — not yet modeled) and 1 Discovery-level
naming decision flagged as not yet exercised (Batch vs. Lot). This table
extends, and must be read alongside, `.claude/context/glossary.md`'s
existing Draft/Accepted terms — it does not replace them.
