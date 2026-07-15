# Constraints

**الحالة العامة للملف:** قيود مؤكدة ومبدئية (Draft/Confirmed) فقط — ليست قائمة
نهائية شاملة.

## الغرض من الملف

تسجيل القيود المعروفة والمؤكدة التي يجب أن تحترمها أي قرارات معمارية لاحقة، تمييزًا
عن المبادئ (`architecture-principles.md`) التي هي توجهات مرغوبة وليست قيودًا صارمة
بالضرورة.

## القالب المتوقع لكل قيد

- **Constraint**: نص القيد.
- **Type**: Technical / Regulatory / Organizational / Ethical.
- **Status**: Confirmed (من وصف المشروع) أو Draft (يحتاج تأكيد).

## طريقة التحديث

أضف قيدًا جديدًا فقط عندما يكون مؤكدًا من صاحب المشروع أو ناتجًا عن قرار Accepted؛
لا تُضِف قيودًا افتراضية أو مُخمَّنة.

---

## القيود المؤكدة والمبدئية الحالية

| # | القيد | النوع |
|---|---|---|
| 1 | يجب أن يكون النظام قابلًا للتوسع (Scalable) | Technical |
| 2 | يجب دعم فرق مستقلة تعمل على Modules منفصلة | Organizational |
| 3 | يجب ألا يعتمد Module على تفاصيل تنفيذ Module آخر (Avoid Direct Coupling) | Technical |
| 4 | الصلاحيات (Authorization) يجب تطبيقها في Backend، وليس فقط في الواجهة | Technical/Security |
| 5 | البيانات الطبية شديدة الحساسية | Regulatory/Ethical |
| 6 | لا يجوز أن يُصدر AI تشخيصًا طبيًا نهائيًا بصورة مستقلة دون مراجعة بشرية | Ethical/Regulatory |
| 7 | لا يُعتمد Microservices كخيار افتراضي من البداية (Modular Monolith First) | Technical |

## قيود جديدة أُضيفت بعد اعتماد Constitution v1 (2026-07-15)

هذه القيود ناتجة مباشرة عن قرارات **Accepted** ضمن
`docs/constitution/PROJECT-CONSTITUTION.md` v1 وADRs المقابلة لها — وليست قيودًا
مُخمَّنة.

| # | القيد | النوع | ADR |
|---|---|---|---|
| 8 | لا يجوز لأي Module الوصول المباشر (SQL joins/writes) لجداول/schema مملوكة لـModule آخر — الوصول فقط عبر API/Events/Read Models معتمدة | Technical | [0003](../../docs/adr/0003-schema-per-module.md) |
| 9 | يجب أن يكون عزل المستأجرين (Tenant Isolation) قابلًا للاختبار آليًا (automated) قبل اعتبار أي Module يتعامل مع بيانات مستأجرين "منتهيًا" | Technical | [0005](../../docs/adr/0005-hybrid-tenant-isolation.md) |
| 10 | يجب أن تحتفظ محولات تكامل الأجهزة الطبية (Device Adapters) بمصدر ومصدرية (Provenance) كل نتيجة مستوردة، ولا يجوز لعطل جهاز أن يُفسد بيانات العمل الأساسية | Technical/Regulatory | [0006](../../docs/adr/0006-independent-device-gateway.md) |
| 11 | لا يجوز إرسال بيانات حساسة إلى مزوّد AI خارجي دون سياسة وضوابط معتمدة مسبقًا | Ethical/Regulatory | [0007](../../docs/adr/0007-governed-ai-gateway.md) |
| 12 | إخفاء عنصر واجهة (UI hiding) لا يُعتبر أبدًا ضابط تفويض (Authorization Control) | Technical/Security | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| 13 | يجب أن يبقى مزوّد الـCloud قابلًا للاستبدال حيثما أمكن عمليًا، ويجب أن يكون Data Residency قابلًا للتهيئة حسب السوق | Technical/Regulatory | [0009](../../docs/adr/0009-saas-first-on-premise-and-hybrid-ready.md) |
| 14 | لا يجوز لأي نموذج بيانات أو عقد (Contract) أن يفترض لغة/عملة/منطقة زمنية واحدة بشكل ثابت (Hardcoded) | Technical | [0010](../../docs/adr/0010-arabic-english-and-localization-first.md) |

## ملاحظة

قيود إضافية (تنظيمية، جغرافية، أداء) ستُضاف بعد الإجابة على الأسئلة في
`open-questions.md`. القيود 1–7 لم تُحذف ولم تتغيّر — القيود 8–14 إضافة جديدة فقط.
