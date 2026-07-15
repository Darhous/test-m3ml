# Architecture Principles

**الحالة العامة للملف:** Draft — هذه مبادئ أولية موجهة للنقاش، **ليست نهائية (Final)**،
ولا تشكّل بحد ذاتها Software Architecture Document.

## الغرض من الملف

تجميع المبادئ المعمارية العالية المستوى (High-Level Principles) التي يُفترض أن
تسترشد بها القرارات المعمارية اللاحقة. كل مبدأ هنا يحتاج مناقشة وتفصيل واعتماد عبر
ADR عندما يتحول من Draft إلى قرار مُلزم.

## القالب المتوقع لكل مبدأ

- **Principle**: اسم المبدأ.
- **Meaning**: ماذا يعني عمليًا.
- **Status**: Draft / Proposed / Accepted.
- **Related ADR**: (يُملأ لاحقًا عند الاعتماد الرسمي).

## طريقة التحديث

عند مناقشة مبدأ ومقارنته بخيارات بديلة، أنشئ ADR له عبر skill
`architecture-decision-records`، ثم حدّث حالته هنا إلى `Accepted` واربطه بالـADR.

---

## Draft Principles (منقولة من وصف المشروع الأولي — غير معتمدة بعد)

| # | Principle | الحالة |
|---|---|---|
| 1 | Modular Monolith First | Draft |
| 2 | Selective Service Extraction when justified | Draft |
| 3 | Domain-Driven Design | Draft |
| 4 | Clear Bounded Contexts | Draft |
| 5 | Backend-Enforced Authorization | Draft |
| 6 | Least Privilege | Draft |
| 7 | Explicit Data Scopes | Draft |
| 8 | Event-Driven Integration | Draft |
| 9 | API-First Design | Draft |
| 10 | Auditability by Default | Draft |
| 11 | Secure by Design | Draft |
| 12 | Privacy by Design | Draft |
| 13 | Human-in-the-Loop for sensitive medical AI actions | Draft |
| 14 | Avoid Direct Module Coupling | Draft |
| 15 | Contracts over implementation sharing | Draft |
| 16 | Configuration over hardcoded workflows | Draft |
| 17 | Multi-Tenant Readiness | Draft |
| 18 | Observability by Default | Draft |
| 19 | Backward-Compatible Evolution | Draft |

## ملاحظة

هذه القائمة **مبدئية وغير مرتبة بالأولوية**. الترتيب والتفصيل والتعارضات المحتملة
بين المبادئ (مثلاً: Modular Monolith First مقابل Multi-Tenant Readiness) تحتاج نقاشًا
مخصصًا لاحقًا، وليست جزءًا من هذه المهمة.
