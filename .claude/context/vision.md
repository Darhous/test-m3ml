# Vision

**الحالة:** Draft — راجع `.claude/context/README.md` لشرح نظام الحالات.

## الغرض من الملف

تسجيل الرؤية العامة للمنصة والهدف طويل المدى، كما وردت في وصف المشروع حتى الآن.
هذا ليس رؤية نهائية معتمدة (Accepted) — هو التقاط أولي (Initial Confirmed Context)
لما تم ذكره صراحة، قابل للتوسعة والمراجعة.

## القالب المتوقع

- **What**: ما هي المنصة؟
- **Starting point**: أين تبدأ فعليًا؟
- **Long-term goal**: إلى أين تتجه؟
- **Core platform shape**: ما الذي يجمع كل شيء معًا؟
- **User routing model**: كيف يصل المستخدم لواجهته الصحيحة؟
- **Non-goals / clarifications**: ما الذي **ليس** المنصة؟

## طريقة التحديث

أضف بندًا جديدًا مع الحالة (Draft/Proposed/Accepted) عند توسّع الرؤية أو تدقيقها في
جلسة نقاش لاحقة. لا تُضِف تفاصيل تنفيذية (تقنيات، أطر عمل) هنا — هذا ملف رؤية وليس
قرارات تقنية (انظر `decisions.md` و `architecture-principles.md`).

---

## Initial Confirmed Context (Draft)

- المشروع **منصة صحية رقمية متكاملة (Digital Healthcare Platform)**.
- نقطة البداية الفعلية هي **إدارة المعامل الطبية (Laboratory Management)**.
- الهدف طويل المدى: **Healthcare Platform** واسعة وقابلة للتوسع تتجاوز نطاق المعامل.
- يوجد **Backend Platform مركزي** يخدم جميع الواجهات.
- توجد **واجهة دخول موحدة (Unified Login)** لجميع المستخدمين.
- يتم توجيه المستخدم بعد الدخول إلى **Portal أو Dashboard** مناسبة بناءً على:
  - Role
  - Permissions
  - Data Scope
  - Organization
  - Branch
- المنصة **ليست مجرد CRUD** — يُفهم من هذا وجود منطق أعمال ومعالجة أعمق (Workflows,
  Domain Logic) وليست عمليات إدخال/عرض بيانات بسيطة فقط.
- الاتجاه المبدئي المعماري: **Modular Architecture**.
- خصائص مطلوبة للمنصة (كأهداف عامة، غير مفصّلة بعد):
  - **API-First**
  - **Event-Driven**
  - **AI-Ready**
  - **Integration-Ready**

## Expanded Vision — Healthcare Operations Platform (Confirmed, User-Directed, 2026-07-16)

المستخدم وسّع الرؤية صراحةً ضمن "Discovery Gap Closure & Healthcare
Operations Platform Expansion" (راجع `docs/discovery/artifacts/
W1-vision-scope-operating-model.md` للتفاصيل الكاملة). هذا القسم **Confirmed**
لأنه منقول حرفيًا من تعليمات المستخدم الصريحة، وليس Inferred:

- المنتج المستهدف ليس LIMS أو Laboratory Management System أو Patient
  Results Portal أو Billing System فقط — بل **Healthcare Operations
  Platform**: منصة SaaS Multi-Tenant تدير تشغيل المؤسسات الصحية
  والتشخيصية.
- السوق الأول: **مصر**، مع جاهزية معمارية لأسواق إضافية لاحقًا.
- أنواع العملاء المستهدفة (Confirmed): معمل مستقل، سلسلة معامل، مستشفى،
  مركز طبي، عيادة، مجموعة طبية، Corporate Healthcare Provider، جهة
  تشخيصية متعددة الفروع، Partner/API Client خارجي.
- 32 مجال أعمال (Business Domains) يجب أن تغطيها Discovery الكاملة — القائمة
  الكاملة في `docs/discovery/artifacts/W1-vision-scope-operating-model.md`.
  الـBaseline Discovery (Phases 02–12) غطّت بعمق حقيقي 4 مجالات فقط من أصل
  32؛ الباقي مستهدف عبر Waves 3–12 من برنامج Gap Closure.
- التزامات تشغيلية جديدة Confirmed: White Label، Plans and Subscriptions،
  Usage/Entitlement Tracking، SaaS billing readiness — لا تتعارض مع أي
  قرار Accepted سابق (تم التحقق).
- لا يُفترض بناء ERP مالي كامل بالضرورة في الإصدار الأول (تعليمات مستخدم
  صريحة) — الحدود بين Native/Integration/Deferred للنطاق المالي تُكتشف في
  Wave 3/10 من Gap Closure، وليست مفترضة هنا.

## Open items

راجع `open-questions.md` للأسئلة التي يجب الإجابة عليها قبل ترسيخ هذه الرؤية.
