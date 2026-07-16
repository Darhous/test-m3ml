# Stakeholders

**الحالة العامة للملف:** Draft — فئات أولية، بدون تفصيل احتياجات كل فئة بعد.

## الغرض من الملف

تجميع فئات أصحاب المصلحة (Stakeholders) المعروفة حتى الآن، كمدخل لتحديد
Bounded Contexts وواجهات الاستخدام (Portals/Dashboards) لاحقًا.

## القالب المتوقع لكل فئة (عند التفصيل لاحقًا)

- **Stakeholder**: اسم الفئة.
- **Primary needs**: (فارغ حتى تُناقَش).
- **Related Portal/Dashboard**: (يُملأ لاحقًا).
- **Status**: Draft.

## طريقة التحديث

لا تُضِف احتياجات تفصيلية مخمّنة لكل فئة الآن. عند نقاش فعلي لاحتياجات فئة معينة،
وسّع القسم الخاص بها مع تحديد الحالة (Draft/Proposed/Accepted).

---

## الفئات الأولية

1. Patients
2. Doctors
3. Laboratory Staff
4. Laboratory Management
5. Organization Administrators
6. Platform Administrators
7. Finance Teams
8. Inventory Teams
9. Insurance Users
10. Suppliers
11. Device Integration Teams
12. Support Teams
13. Security and Compliance Teams
14. Development Teams
15. External API Partners

## ملاحظة

هذه القائمة أولية وقد تحتاج تقسيمًا أدق لاحقًا (مثلًا: تمييز Lab Technician عن
Lab Manager ضمن Laboratory Staff) عند التعمق في تصميم الأدوار والصلاحيات.

## Discovery Phase 02 — Candidate Needs (Assumption-Driven Run)

**تنبيه صريح:** البنود أدناه **ليست** نتيجة نقاش فعلي مع أصحاب المصلحة —
هي `Inferred — Industry Reference` فقط (معرفة عامة عن صناعة المعامل
الطبية)، أُنتجت ضمن Discovery Phase 02 بعد موافقة صريحة من المستخدم على
"Assumption-Driven Autonomous Run" (انظر
`docs/discovery/reports/00-discovery-program-status-report.md`). هذا لا
يُخالف قاعدة الملف أعلاه ("لا تُضِف احتياجات مخمّنة")، لأنها هنا موسومة
بوضوح كـ Inferred وليست معروضة كنتيجة نقاش حقيقي — تحتاج مراجعة وتأكيد
فعلي من المستخدم قبل اعتبارها Accepted أو حتى Proposed.

| # | Stakeholder | Candidate Primary Needs (Inferred) | Related Value Stream(s) | Status |
|---|---|---|---|---|
| 1 | Patients | Convenient test ordering/booking; trustworthy, timely results; clear billing | VS1, VS2, VS3, VS4 | Inferred — Industry Reference |
| 2 | Doctors | Fast, reliable result delivery; ability to order on behalf of a patient; result history access | VS1, VS2 | Inferred — Industry Reference |
| 3 | Laboratory Staff | Clear worklists; accurate specimen tracking; low-friction result entry/verification | VS1, VS2, VS3 | Inferred — Industry Reference |
| 4 | Laboratory Management | Operational visibility (throughput, rejection rate); staff workload balancing | VS1, VS2, VS3 | Inferred — Industry Reference |
| 5 | Organization Administrators | Branch-level oversight; user/role administration within their Organization | (cross-cutting) | Inferred — Industry Reference |
| 6 | Platform Administrators | Cross-organization oversight; platform health and configuration | (cross-cutting) | Inferred — Industry Reference |
| 7 | Finance Teams | Accurate invoicing; reconciliation with insurance payments | VS4 | Inferred — Industry Reference |
| 8 | Inventory Teams | Reagent/supply visibility; low-stock alerts tied to test volume | (supports VS1/VS2) | Inferred — Industry Reference |
| 9 | Insurance Users | Clear eligibility/coverage determination; claim status visibility | VS4 | Inferred — Industry Reference |
| 10 | Suppliers | Predictable ordering/replenishment signals from the platform | (supports Inventory capability) | Inferred — Industry Reference |
| 11 | Device Integration Teams | Reliable device connectivity; clear failure diagnostics | VS1, VS2 | Inferred — Industry Reference; reinforced by Constitution Section 24 |
| 12 | Support Teams | Tools to resolve patient/doctor issues (rebooking, rejected specimens) | VS3 | Inferred — Industry Reference |
| 13 | Security and Compliance Teams | Full audit trail; enforceable Data Scope; breach-readiness visibility | (cross-cutting) | Inferred — Industry Reference; reinforced by Constitution Section 21/23 |
| 14 | Development Teams | Clear module boundaries and contracts to build against | (cross-cutting) | Inferred — Industry Reference; reinforced by Constitution Section 5–9 |
| 15 | External API Partners | Stable, versioned integration contracts | (supports VS4, future integrations) | Inferred — Industry Reference; reinforced by Constitution Section 14–15 |

**التالي:** يجب على المستخدم مراجعة هذا الجدول وتأكيد/تصحيح/رفض كل بند قبل
أي استخدام معماري نهائي له (انظر `ASSUMPTION-REGISTER.md`).

## Gap Closure Wave 2 — Expanded Persona Catalog (2026-07-16)

القائمة أعلاه (15 فئة) وسّعت إلى **39 Persona** ضمن برنامج Discovery Gap
Closure، تغطي فئات لم تكن موجودة إطلاقًا في Discovery السابقة: Financial
(Cashier, Accountant, Finance Manager), Workforce (HR, Payroll), Supply
Chain (Procurement, Inventory, Store Manager), Platform/SaaS (Platform
Operator, Tenant/Branch Administrator, SaaS Commercial Team), Governance
(Auditor, Compliance Staff, Legal Reviewer, Regulator). التفاصيل الكاملة
(Goals/Pain Points/Data Scope/High-Risk Actions/KPI لكل Persona) في
`docs/discovery/artifacts/W2-persona-catalog.md`. الفئات الأصلية أعلاه
(1–15) **لم تُحذف** — هذا توسيع، وليس استبدالًا.
