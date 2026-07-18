# Open Questions

**الحالة العامة للملف:** أسئلة مفتوحة تحتاج إجابة قبل اعتماد قرارات معمارية نهائية.

## الغرض من الملف

تجميع الأسئلة غير المجابة التي تؤثر على القرارات المعمارية (خصوصًا Multi-Tenancy،
النطاق الجغرافي/القانوني، والاستضافة)، بحيث لا تُتخذ قرارات مبنية على افتراضات غير
مؤكدة.

## القالب المتوقع لكل سؤال

- **Question**: السؤال.
- **Why it matters**: أثره على القرارات المعمارية.
- **Status**: Open / Answered (مع الإحالة إلى مكان الإجابة عند توفرها).

## طريقة التحديث

عند الإجابة على سؤال، انقله من هنا إلى الملف المناسب (`constraints.md`,
`decisions.md`, `vision.md`...) مع تحديد حالته، واترك إشارة هنا إلى أنه Answered
ومكان الإجابة.

---

## Open Questions (بلا إجابات مؤكدة بعد)

1. ما الدول والأسواق المستهدفة؟
2. ما المتطلبات القانونية المحلية (تنظيمية/صحية/حماية بيانات)؟
3. هل الاستضافة Cloud أم On-Premise أم Hybrid؟
4. ما حجم الاستخدام المتوقع (عدد المستخدمين، المعاملات، المعامل)؟
5. ما أنواع أجهزة المعامل المطلوب دعمها (Device Integration)؟
   **[Discovery Phase 08]** فئات بروتوكول مرشّحة (غير مؤكدة): HL7 v2, ASTM,
   Vendor API — مبنية على قائمة الجاهزية المعتمدة في Constitution Section
   24، وليست تأكيدًا لجهاز فعلي. انظر
   `docs/discovery/artifacts/08-integration-inventory.md`.
6. هل يوجد Offline Mode مطلوب؟
   **[Discovery Phase 08]** اقتُرح نمط تصميم "Local-first capture + eventual
   sync" لجهاز الجمع المنزلي المحمول، **كحل تصميمي محتمل فقط إن تأكدت
   الحاجة** — لا يُجيب هذا على أصل السؤال (هل Offline Mode مطلوب أصلًا).
7. ما استراتيجية Multi-Tenancy المطلوبة (Tenant per DB, Shared DB with Tenant ID, ...)؟
8. ما نوع عزل البيانات المطلوب بين المؤسسات (Organizations)؟
9. هل سيتم دعم المستشفيات والعيادات من النسخة الأولى، أم المعامل فقط في البداية؟
10. ما قنوات الإشعارات المطلوبة (SMS, Email, Push, WhatsApp...)؟
    **[Discovery Phase 08]** رُشِّحت قنوات محتملة (SMS، Push، Email،
    إشعار داخل الـPortal، WhatsApp) بناءً على احتياجات أصحاب المصلحة
    المستنتجة (Phase 02) — **لا تزال غير مؤكدة**. انظر
    `docs/discovery/artifacts/08-integration-inventory.md`.
11. ما حدود استخدام AI (خصوصًا فيما يخص القرارات الطبية والـHuman-in-the-Loop)؟
    **[Discovery Phase 10]** حدود القاعدة العامة (Constitution Section 28)
    ثابتة ومعتمدة أصلًا. ما أُضيف هنا: 7 حالات استخدام مرشّحة بحدود HITL
    محددة، حالة واحدة رُفضت صراحةً (اعتماد تلقائي للنتائج الطبيعية)، وحالة
    واحدة "غير جاهزة" (تلخيص إشعارات دون مراجعة دقة). لا تُعتبر أي حالة من
    السبع Accepted — تنتظر Phase 11/12. انظر
    `docs/discovery/artifacts/10-ai-use-case-catalog.md`.
12. ما اللغات والعملات المطلوب دعمها؟
13. هل توجد أنظمة حالية (Legacy Systems) يُطلب ترحيل بيانات منها؟
    **[Discovery Phase 08]** لا يوجد أي أساس (مؤكد أو مُستنتج) للإجابة —
    لم يُخترع أي ملف تعريف لنظام قديم؛ يبقى فارغًا تمامًا حتى تتوفر مدخلات
    حقيقية.

## أسئلة جديدة أُضيفت أثناء إعداد Constitution v1 (2026-07-15)

14. **ما هو الـCore Domain للمنصة؟** (Strategic Design/Distillation ضمن DDD — انظر
    `docs/constitution/PROJECT-CONSTITUTION.md` Section 6 و46). لم يُحدَّد بعد؛
    يحتاج جلسة DDD مخصصة عند بدء اكتشاف الـModules الفعلية. **لا** يُعتبر أي
    Bounded Context "Core" ضمنيًا لمجرد ذكره في `module-catalog.md`.
    **Proposed answer (Discovery Phase 04, Assumption-Driven، غير معتمد):**
    "Test Processing and Result Verification" — انظر
    `docs/discovery/artifacts/04-subdomain-map.md` للأدلة والمنطق. يبقى
    البند **Open** حتى تجتاز Phase 11 (Validation) وتُصادَق عليه في Phase 12
    عبر ADR.
    **[Gap Closure Wave 7]** أُعيد تقييم الإجابة المقترحة مقابل 6 بدائل
    (Diagnostic Operations, Patient-to-Result Orchestration, Laboratory
    Execution, Healthcare Operations Orchestration, Clinical Diagnostic
    Network, Platform Tenant Operations). التوصية الجديدة (Recommended,
    غير معتمدة): **"Patient-to-Result Orchestration"** تحل محل الصياغة
    الأضيق — انظر `docs/discovery/artifacts/
    W7-domain-classification-reevaluation.md` للـDecision Matrix الكامل.
    القرار النهائي (Retain/Amend/Supersede/Reject لـADR-0011) يُحسم في
    Wave 14.
15. **ما التقنية الافتراضية الدقيقة لتقسيم البيانات في الطبقة المشتركة (Shared
    tier)** ضمن Hybrid Tenant Isolation (ADR 0005) — مثل tenant ID column مقابل
    schema منفصل؟ Constitution v1 حسم النموذج الثنائي (Shared/Dedicated) لكن ترك
    التفصيل التقني للـSoftware Architecture Document لاحقًا.
    **[Discovery Phase 09]** ضِيق الخيار إلى فئتين مرشّحتين (Tenant-identifier
    column، أو Schema-per-tenant داخل نفس قاعدة البيانات المشتركة)، مع توضيح
    أن هذا محور مستقل عن Schema per Module (ADR 0003). لم يُحسم أي منهما.
    انظر `docs/discovery/artifacts/09-tenancy-analysis.md`.
16. **ما مسار الترقية (Promotion Path)** لمستأجر ينتقل من الطبقة المشتركة إلى
    الطبقة المخصصة ضمن Hybrid Tenant Isolation؟ لم يُحسم بعد.
    **[Discovery Phase 09]** اقتُرح نوع المُحفِّز (Trigger Type) دون رقم محدد:
    استهلاك موارد مُقاس ومستدام، أو متطلب تعاقدي/تنظيمي — يتوافق مع أسلوب
    Constitution Section 55 (Evolution Strategy). لا رقم أو عتبة مُخترعة.

## أسئلة جديدة أُضيفت أثناء Discovery Phase 02 (Business Discovery)

17. **ما نموذج الفوترة/التأمين الفعلي؟** (Direct billing مقابل Reimbursement
    مقابل Capitation، إلخ) — ظهر أثناء تتبع Value Stream 4 (Insurance Claim
    Billing Cycle، `docs/discovery/artifacts/02-value-streams.md`)، ولا
    توجد إجابة مؤكدة. لم يُفترض نموذج معين.

## أسئلة جديدة أُضيفت أثناء Discovery Phase 07 (Business Rules)

18. **ما هي المدة الزمنية الفعلية لانتهاء صلاحية طلب الفحص (Order Expiry)**
    إذا لم تُجمع العيّنة؟ لا يوجد أساس لافتراض رقم — انظر
    `docs/discovery/artifacts/07-business-rules-catalog.md` (H3).
19. **ما معايير الأهلية الدقيقة لاعتماد النتائج (Result Verifier Role)؟**
    (مثلًا: هل يلزم Pathologist لكل أنواع الفحوصات أم فقط لبعضها؟) —
    **أولوية عالية** لتأثيرها المباشر على السلامة السريرية (H1، مرتبط بـ
    Constitution Section 21).
20. **ما عتبة تصعيد الرفض المتكرر لنفس الطلب (N)؟** (H7)
21. **ما سياسة التعافي عند فشل المعالجة/عطل الجهاز أثناء التحليل؟** (H2)
22. **ما سياسة إعادة المحاولة عند فشل زيارة جمع العيّنة المنزلية؟** (H4)

## أسئلة جديدة أُضيفت أثناء Gap Closure Wave 6 (Business Rules and Policy Discovery)

23. **ما القيم الفعلية لمحاور سياسة اعتماد النتائج القابلة للتهيئة** (نوع
    المؤسسة، نوع التحليل، درجة الخطورة، التخصص، Branch/Country Policy)؟
    النموذج نفسه مصمّم (`docs/discovery/artifacts/
    W6-business-rules-and-policy-catalog.md`)، لكن القيم فارغة تمامًا —
    **أولوية عالية**، مرتبطة مباشرة بالسؤال #19.
24. **هل يلزم مستوى "Elevated Audit" ثانٍ أوسع من Sensitive Operations** (يشمل
    Refund، Expiry-block، Break-Glass، Tenant Configuration)؟ Recommendation
    مطروحة، غير معتمدة.

## أسئلة جديدة أُضيفت أثناء Gap Closure Wave 11 (Egypt Market Gap Analysis)

25. **ما أحكام النقل عبر الحدود (Cross-Border Transfer) الفعلية ضمن قانون
    حماية البيانات الشخصية المصري (151/2020)؟** لم تُراجَع النصوص الأولية
    بعمق — `Requires Legal Verification`. انظر
    `docs/discovery/artifacts/EGYPT-REGULATORY-RESEARCH-REGISTER.md` #2.
26. **ما متطلبات قانون العمل/التأمينات الاجتماعية المصري المؤثرة على
    Payroll؟** لم يُبحث هذا الجانب في هذه الجولة إطلاقًا —
    `Requires Legal Verification`، فجوة بحثية صريحة.
27. **هل يجب أن يكون الرقم القومي (National ID) حقلًا أساسيًا في Patient
    Management؟** Recommendation مطروحة، غير مؤكدة — تحتاج بحثًا عن قواعد
    ربط الهوية الصحية المصرية.

## أسئلة جديدة أُضيفت أثناء API Platform & Developer Ecosystem Strategy – Part 1 (2026-07-18)

28. **ما منتج API Gateway المحدد الذي سيُعتمد؟** (مثل Kong, Tyk, KrakenD,
    Envoy, Apigee...) — لا يوجد أي منتج API Gateway مُقيَّم أو مُعتمَد ضمن
    الـTechnology Baseline المُجمَّد (21 Engine). "Public API Gateway" مذكور
    في Constitution Section 11 كـ**دور معماري** (Independent Component)
    فقط، وليس قرار تقنية. اختيار منتج فعلي هو قرار Build-vs-Buy يقع خارج
    صلاحية `docs/api-platform/` (انظر `10-API-GATEWAY.md`). لا يُفترض أي
    منتج بالتخمين.
29. **ما محرك إدارة الأسرار (Secrets/Vault Engine) الذي سيُعتمد؟** (مثل
    HashiCorp Vault, Infisical...) — نفس الفجوة أعلاه، لا يوجد أي محرك
    Secrets/Vault ضمن الـTechnology Baseline. انظر `docs/api-platform/
    12-SECRETS-AND-KEYS.md` للمتطلبات السلوكية المطلوبة من أي محرك
    مستقبلي، دون تحديد منتج.

## ملاحظة

هذه القائمة أولية وستنمو مع تقدم النقاش. لا تُفترض إجابات لهذه الأسئلة ولا تُبنى
عليها قرارات Accepted قبل توثيق الإجابة الفعلية. الأسئلة 1–13 لم تُحذف ولم تُجَب
أثناء إعداد Constitution v1 — Constitution v1 حسمت مبادئ حاكمة عليا (Modular
Monolith, DDD, Tenancy shape, إلخ) دون الحاجة لإجابة كل سؤال هنا أولًا، لكنها لم
تُجب فعليًا على أي من الأسئلة 1–13 نفسها.
