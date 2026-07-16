# Module Catalog

**الحالة العامة للملف:** Draft — تصنيفات أولية فقط، **ليست القائمة النهائية**
للـModules.

## الغرض من الملف

تجميع تصنيفات عالية المستوى (Categories) للـModules المحتملة في المنصة، كنقطة
انطلاق لنقاش Bounded Contexts لاحقًا (باستخدام skill `domain-driven-design`)، دون
الدخول في تفاصيل كل Module أو قائمته النهائية.

## القالب المتوقع لكل تصنيف (عند التفصيل لاحقًا)

- **Category**: اسم التصنيف.
- **Candidate Modules**: (فارغ حتى تُناقَش بالتفصيل).
- **Related Bounded Context(s)**: (يُملأ عند تطبيق skill `domain-driven-design`).
- **Status**: Draft.

## طريقة التحديث

لا تُضِف Modules فردية تفصيلية هنا الآن. عند البدء الفعلي بتصميم Bounded Contexts،
استخدم skill `domain-driven-design` + `c4-architecture`، ووثّق النتائج في وثيقة
منفصلة (أو وسّع هذا الملف حينها بموافقة صريحة).

---

## التصنيفات الأولية (Categories only — بدون تفصيل Modules)

1. Core Platform Modules
2. Identity and Access Modules
3. Organization Modules
4. Patient Modules
5. Doctor and Clinic Modules
6. Laboratory Modules
7. Device Integration Modules
8. Workflow Modules
9. Notification and Communication Modules
10. Billing and Finance Modules
11. Insurance Modules
12. Inventory and Procurement Modules
13. AI and Analytics Modules
14. Integration Modules
15. Security and Compliance Modules
16. Support and Operations Modules

## ملاحظة

هذه تصنيفات **مبدئية غير نهائية**، ولا تمثل التزامًا بعدد أو حدود الـModules
الفعلية. القائمة النهائية للـModules تتطلب جلسة تصميم DDD مخصصة.

## Candidate Contexts from Discovery (Phase 06, Assumption-Driven Run)

**تنبيه صريح: هذه مرشّحات من Discovery (`docs/discovery/artifacts/
06-bounded-contexts.md`)، وليست القائمة النهائية.** جلسة DDD الفعلية
المذكورة أعلاه هي بالضبط Discovery Phase 04–06 التي نُفِّذت، لكن بأسلوب
Assumption-Driven (بدون مدخلات فعلية من أصحاب مصلحة حقيقيين) — لذلك تبقى
هذه مرشّحات تحتاج مراجعة، لا اعتمادًا نهائيًا.

| # | Discovery Candidate Context | يقابل تصنيف(ات) | ملاحظة |
|---|---|---|---|
| 1 | Order Management | جزء من #6 Laboratory Modules | تقسيم أدق |
| 2 | Specimen Management | جزء من #6 Laboratory Modules | تقسيم أدق |
| 3 | Test Processing and Result Verification (**Core Domain مرشّح**) | جزء من #6 Laboratory Modules | تقسيم أدق؛ أقوى مرشّح لـ Core Domain |
| 4 | Notification and Communication | #9 Notification and Communication Modules | تطابق مباشر |
| 5 | Billing and Claims | #10 Billing and Finance Modules + #11 Insurance Modules | دمج التصنيفين #10 و#11 |
| 6 | Device and Equipment Integration | #7 Device Integration Modules | تطابق مباشر |
| 7 | Core Platform — Identity and Access | #1 Core Platform Modules + #2 Identity and Access Modules | دمج التصنيفين |
| 8 | Core Platform — Organization and Branch | #3 Organization Modules | تطابق مباشر |

**تصنيفات لم تُغطَّ بعد بدليل حقيقي:** #4 Patient Modules، #5 Doctor and
Clinic Modules (لا يوجد Bounded Context مستقل بعد — Patient/Doctor ما زالا
Actors فقط)، #8 Workflow Modules (سلوك عابر ضمن Specimen/Test Processing،
وليس Context مستقل)، #12 Inventory and Procurement، #13 AI and Analytics
(مهمة Phase 10)، #14 Integration Modules (يتداخل مع #6 أعلاه + نتائج Phase
08)، #15 Security and Compliance (يتوزع بين #7 أعلاه والحوكمة على مستوى
Constitution)، #16 Support and Operations — **لا دليل Event Storming كافٍ
بعد** (انظر `docs/discovery/artifacts/04-subdomain-map.md`).

**لا يزال هذا الملف غير نهائي** — القائمة النهائية تنتظر Phase 11
(Validation) وPhase 12 (Final Discovery Book)، وحتى بعدها تبقى "مرشّحة" لا
نهائية إلا بموافقة صريحة من المستخدم، حسب Constitution Section 2/46.

## Gap Closure Wave 3 — Enterprise Capability Map (2026-07-16)

الجدول أعلاه (8 Contexts، من Laboratory-only Discovery) يُعاد تقييمه الآن
ضمن خريطة قدرات مؤسسية كاملة: **100 Capability** عبر 10 فئات (Clinical,
Laboratory Operations, Workforce, Financial, Supply Chain, Asset/Device,
Customer Operations, SaaS/Platform, Governance, Data/Intelligence) —
التفاصيل الكاملة في `docs/discovery/artifacts/W3-enterprise-capability-map.md`.
هذا **لا يُلغي** التصنيفات الثمانية أعلاه؛ Wave 9 من برنامج Gap Closure
تعيد بناء Context Map الكاملة بناءً على هذه القدرات الموسّعة. لا يزال
الملف Candidate غير نهائي.
