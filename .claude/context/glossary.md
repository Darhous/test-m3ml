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

## Accepted Definitions (من Constitution v1)

المصطلحات التالية عرّفتها `docs/constitution/PROJECT-CONSTITUTION.md` v1 (Section
47) صراحةً ولم تكن موجودة في القائمة الأصلية أعلاه. حالتها **Accepted** لأنها جزء من
Constitution معتمدة، عدا "Core Domain" الذي يبقى Open حتى تُحدَّد جلسة DDD مخصصة.

| Term | Definition | Status | Related ADR |
|---|---|---|---|
| Independent Component | مكوّن (Notification Service, Device Integration Gateway, AI Gateway, Analytics Platform, Search Service, File Processing Service, Public API Gateway, Background Workers) يُسمح له بأن يكون مستقلًا تشغيليًا من الإصدار الأول لسبب موثّق، دون أن يكون ذلك افتراضًا عامًا لصالح Microservices | Accepted | — (Constitution Section 11) |
| Hybrid Tenant Isolation | نموذج عزل ثنائي المستوى: بنية تحتية مشتركة مع عزل منطقي صارم للمستأجرين الصغار/المتوسطين، وقاعدة بيانات أو نشر مخصص كخيار للمستأجرين الكبار/المنظَّمين | Accepted | [0005](../../docs/adr/0005-hybrid-tenant-isolation.md) |
| Break-Glass Access | وصول طارئ استثنائي، محدود زمنيًا، مبرَّر، وخاضع للتدقيق الكامل، يتجاوز مسار التفويض الطبيعي | Accepted | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| Anti-Corruption Layer | طبقة ترجمة تمنع تسرّب نموذج نظام خارجي (جهاز، مزوّد AI، نظام قديم) إلى النموذج الداخلي لأي Bounded Context | Accepted | [0006](../../docs/adr/0006-independent-device-gateway.md), [0007](../../docs/adr/0007-governed-ai-gateway.md) |
| Core Domain | الـBounded Context (أو أكثر) الذي تكمن فيه القيمة التنافسية/المميِّزة للمنصة، ويستحق أعمق استثمار في النمذجة | **Open** — لم يُحدَّد بعد؛ يحتاج جلسة DDD مخصصة (انظر `open-questions.md` البند 14) | — |

## ملاحظة

هذه تعريفات **أولية جدًا** ومبنية فقط على الوصف العام للمشروع؛ العديد منها يحتاج
دقة إضافية (خصوصًا Tenant/Organization/Branch وعلاقتها بـMulti-Tenancy) بعد الإجابة
على الأسئلة في `open-questions.md`. قسم "Accepted Definitions" أعلاه هو الاستثناء
الوحيد الحالي — تعريفات معتمدة رسميًا ضمن Constitution v1، ولا تُعدَّل دون ADR جديد.

## Discovery Phase 03 — Candidate Ubiquitous Language (Event Storming)

**Inferred — Industry Reference**, من `docs/discovery/artifacts/
03-event-storming-board.md`. Draft فقط — لم تُراجَع مع مستخدمين حقيقيين.

| Term | Draft Definition | Status |
|---|---|---|
| TestOrdered | حدث يمثل طلب فحص من طبيب أو مريض | Draft — Inferred |
| SpecimenCollected | حدث يمثل جمع عيّنة من مريض في الفرع | Draft — Inferred |
| SpecimenAccessioned | حدث يمثل استلام وتسجيل عيّنة رسميًا داخل المعمل | Draft — Inferred |
| SpecimenRejected | حدث يمثل رفض عيّنة لعدم استيفاء معايير الجودة | Draft — Inferred |
| ResultVerified | حدث يمثل اعتماد نتيجة فحص من جهة مخوّلة سريريًا (Pivotal Event / Sensitive Operation مرشّح) | Draft — Inferred |
| ResultReleased | حدث يمثل إتاحة نتيجة معتمدة للمريض/الطبيب (Pivotal Event) | Draft — Inferred |
| ClaimAdjudicated | حدث يصدر من نظام التأمين الخارجي بنتيجة مطالبة (Pivotal Event، أصله خارجي) | Draft — Inferred |
| Sample Collector | دور مرشّح لموظف يقوم بجمع العيّنات في الزيارات المنزلية | Draft — Inferred |
| Pathologist / Result Verifier | دور مرشّح للجهة المخوّلة باعتماد النتائج سريريًا | Draft — Inferred |

## Discovery Phase 04 — Candidate Subdomains

**Inferred — Industry Reference**، من `docs/discovery/artifacts/
04-subdomain-map.md`. تصنيف Core/Supporting/Generic **مرشّح** فقط.

| Term | Draft Definition | Status |
|---|---|---|
| Order Management (Subdomain) | تجميع أعمال يتعلق بطلب الفحوصات وكتالوج الفحوصات | Draft — Inferred, Supporting (Candidate) |
| Specimen Management (Subdomain) | تجميع أعمال دورة حياة العيّنة الكاملة: جمع، نقل، استلام، فحص جودة، رفض/إعادة جمع | Draft — Inferred, Supporting (Candidate، نقاش مفتوح حول احتمالية Core) |
| Test Processing and Result Verification (Subdomain) | تجميع أعمال المعالجة التحليلية واعتماد النتائج وإتاحتها — **مرشّح Core Domain** | Draft — Inferred, **Core (Proposed answer to open-questions.md #14)** |
| Notification and Communication (Subdomain) | تجميع أعمال إشعار المريض/الطبيب عبر القنوات المختلفة | Draft — Inferred, Generic (Candidate) |
| Billing and Claims (Subdomain) | تجميع أعمال الفوترة والمطالبات التأمينية | Draft — Inferred, Supporting (Candidate، أدلة ضعيفة) |
