# Decisions — ADR Index

**الحالة العامة للملف:** فهرس فارغ حاليًا من ناحية ADRs معتمدة رسميًا؛ يحتوي فقط على
قرارات أولية بحالة **Proposed** (غير معتمدة).

## الغرض من الملف

نقطة مركزية للإشارة إلى جميع Architecture Decision Records الخاصة بالمشروع، ولتسجيل
القرارات المرشحة (Proposed) قبل أن تتحول إلى ADR فعلي.

## القالب المتوقع

عند اعتماد قرار فعليًا:
1. استخدم skill `architecture-decision-records` لإنشاء ملف ADR كامل (عادة تحت
   `docs/adr/NNNN-title.md` — المسار الفعلي يُحدَّد عند إنشاء أول ADR حقيقي للمشروع).
2. أضف سطرًا في جدول **ADR Index** أدناه يشير إلى رقم الـADR وعنوانه وحالته.
3. حدّث حالة القرار في قسم "Proposed Decisions" إلى Accepted/Rejected حسب النتيجة.

## طريقة التحديث

لا تُعدَّل حالة أي قرار من Accepted إلى شيء آخر دون ADR جديد يوثق التغيير
(Superseded-by).

---

## ADR Index

| ADR # | العنوان | الحالة | الرابط |
|---|---|---|---|
| — | (لا توجد ADRs معتمدة بعد) | — | — |

## Proposed Decisions (غير معتمدة — Draft/Proposed فقط)

هذه قرارات أولية مطروحة من وصف المشروع، **لم تُدرس بدائلها بعد** ولم تتحول إلى ADR:

| # | القرار المقترح | الحالة |
|---|---|---|
| 1 | Unified Login | Proposed |
| 2 | Role-Based and Policy-Based Access | Proposed |
| 3 | Modular Monolith as Initial Direction | Proposed |
| 4 | Backend Platform shared by Web and Mobile Clients | Proposed |
| 5 | Event-Driven Notifications | Proposed |
| 6 | Central Audit Trail | Proposed |
| 7 | Configurable Workflow Engine | Proposed |
| 8 | Module SDK and Module Template are required | Proposed |

## ملاحظة

لا يوجد حتى الآن أي قرار بحالة **Accepted**. الانتقال من Proposed إلى Accepted يتطلب
نقاشًا مخصصًا وإنشاء ADR رسمي لكل قرار على حدة.
