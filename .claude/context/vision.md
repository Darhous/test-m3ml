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

## Open items

راجع `open-questions.md` للأسئلة التي يجب الإجابة عليها قبل ترسيخ هذه الرؤية.
