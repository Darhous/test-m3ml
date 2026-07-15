# Glossary

**الحالة العامة للملف:** Draft Definitions — تعريفات أولية قابلة للمراجعة، **ليست
نهائية**.

## الغرض من الملف

توحيد المصطلحات (Ubiquitous Language بالمعنى الخاص بـ DDD) المستخدمة في نقاشات
المشروع، لتفادي الالتباس بين الفرق المختلفة (منتج، هندسة، أعمال).

## القالب المتوقع لكل مصطلح

- **Term**: المصطلح.
- **Draft Definition**: تعريف أولي قابل للنقاش.
- **Status**: Draft (افتراضيًا حتى تُراجَع وتُعتمد).

## طريقة التحديث

عند الاتفاق على تعريف نهائي لمصطلح في نقاش معماري، حدّث حالته من Draft إلى Accepted
واربطه بالـADR أو المصدر الذي اعتمده إن وُجد.

---

## Draft Definitions

| Term | Draft Definition | Status |
|---|---|---|
| Tenant | الكيان الأعلى الذي تُعزل بياناته منطقيًا عن الكيانات الأخرى على المنصة (تعريف أولي يحتاج تحديد استراتيجية Multi-Tenancy — انظر `open-questions.md`) | Draft |
| Organization | جهة/منشأة (مثل معمل أو مستشفى) تعمل ضمن Tenant واحد أو أكثر | Draft |
| Branch | فرع تابع لـ Organization | Draft |
| User | مستخدم للمنصة له حساب ضمن واجهة الدخول الموحدة | Draft |
| Role | تصنيف وظيفي يُحدد نوع الوصول العام للمستخدم | Draft |
| Permission | صلاحية محددة ودقيقة (Granular) تُمنح لمستخدم أو Role | Draft |
| Policy | قاعدة تُحدد كيفية تطبيق Permissions حسب سياق (Data Scope, Organization, Branch...) | Draft |
| Data Scope | نطاق البيانات التي يُسمح لمستخدم معين برؤيتها/التعامل معها | Draft |
| Bounded Context | حدود نموذج ولغة محدد ضمن DDD؛ لا يعني بالضرورة Microservice مستقل | Draft |
| Module | وحدة وظيفية ضمن Modular Monolith، مسؤولة عن Bounded Context واحد أو أكثر مرتبط | Draft |
| Core Platform | الأجزاء المشتركة الأساسية التي تخدم جميع الـModules (Identity, Audit, Notifications الأساسية...) | Draft |
| Shared Service | خدمة/قدرة مشتركة يُعاد استخدامها عبر أكثر من Module دون كسر حدود Bounded Context | Draft |
| Domain Event | حدث يعبّر عن تغيّر ذي معنى داخل Bounded Context واحد | Draft |
| Integration Event | حدث يُستخدم للتواصل بين Bounded Contexts/Modules مختلفة | Draft |
| Workflow | تسلسل خطوات أعمال قابل للتهيئة (Configuration over hardcoded workflows) | Draft |
| Portal | واجهة مستخدم مخصصة لفئة معينة من المستخدمين بعد التوجيه من واجهة الدخول الموحدة | Draft |
| Module SDK | مجموعة أدوات/عقود تسمح ببناء Module جديد متوافق مع Core Platform | Draft |
| Module Template | قالب بداية جاهز لإنشاء Module جديد وفق معايير المنصة | Draft |
| Plugin Contract | العقد (Interface/API) الذي يُلزم أي Module أو تكامل خارجي بالتوافق معه | Draft |
| Audit Event | سجل حدث يُستخدم لأغراض التتبع والمساءلة (Auditability by Default) | Draft |
| Human-in-the-Loop | مبدأ يستلزم مراجعة بشرية قبل اعتماد قرارات حساسة (خصوصًا الطبية) صادرة عن AI | Draft |

## ملاحظة

هذه تعريفات **أولية جدًا** ومبنية فقط على الوصف العام للمشروع؛ العديد منها يحتاج
دقة إضافية (خصوصًا Tenant/Organization/Branch وعلاقتها بـMulti-Tenancy) بعد الإجابة
على الأسئلة في `open-questions.md`.
