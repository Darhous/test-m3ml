# Decisions — ADR Index

**الحالة العامة للملف:** يحتوي الآن على 10 ADRs معتمدة رسميًا (Accepted) ضمن
`docs/constitution/PROJECT-CONSTITUTION.md` (v1)، بالإضافة إلى قرارات أخرى ما زالت
**Proposed** (لم تُدرس بعد ولم تتحول إلى ADR).

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
| 0001 | Modular Monolith First | Accepted | `docs/adr/0001-modular-monolith-first.md` |
| 0002 | Domain-Driven Design | Accepted | `docs/adr/0002-domain-driven-design.md` |
| 0003 | Schema per Module | Accepted | `docs/adr/0003-schema-per-module.md` |
| 0004 | Event-Driven Integration | Accepted | `docs/adr/0004-event-driven-integration.md` |
| 0005 | Hybrid Tenant Isolation | Accepted | `docs/adr/0005-hybrid-tenant-isolation.md` |
| 0006 | Independent Device Gateway | Accepted | `docs/adr/0006-independent-device-gateway.md` |
| 0007 | Governed AI Gateway | Accepted | `docs/adr/0007-governed-ai-gateway.md` |
| 0008 | Unified Login and Policy-Based Access | Accepted | `docs/adr/0008-unified-login-and-policy-based-access.md` |
| 0009 | SaaS First, On-Premise Ready, and Hybrid Ready | Accepted | `docs/adr/0009-saas-first-on-premise-and-hybrid-ready.md` |
| 0010 | Arabic/English and Localization First | Accepted | `docs/adr/0010-arabic-english-and-localization-first.md` |

## Accepted Decisions (منقولة من Proposed بعد ADR رسمي)

القرارات التالية كانت مدرجة سابقًا تحت "Proposed Decisions" في هذا الملف، وأصبحت
الآن **Accepted** ضمن `docs/constitution/PROJECT-CONSTITUTION.md` v1، مع ADR مقابل
لكل منها:

| # | القرار (كما كان مطروحًا سابقًا) | الحالة الحالية | ADR |
|---|---|---|---|
| 1 | Unified Login | Accepted (ضمن "Unified Login and Policy-Based Access") | 0008 |
| 2 | Role-Based and Policy-Based Access | Accepted (ضمن "Unified Login and Policy-Based Access") | 0008 |
| 3 | Modular Monolith as Initial Direction | Accepted | 0001 |
| 4 | Backend Platform shared by Web and Mobile Clients | Accepted (ضمن "Unified Login and Policy-Based Access" — Unified Login يفترض Backend Platform مشترك) | 0008 |

القرارات التالية **لم تُدرس بعد بصورة مستقلة** وتبقى Proposed — لم يصدر ADR خاص بها
في هذه الجولة (لا علاقة مباشرة كافية بالقرارات العشرة أعلاه لتُعتبر مغطاة ضمنًا):

| # | القرار المقترح | الحالة |
|---|---|---|
| 5 | Event-Driven Notifications | Proposed (المبدأ العام "Event-Driven Integration" أصبح Accepted عبر ADR 0004، لكن "Notifications" تحديدًا كقرار منتج/تصميم لم يُدرس بعد كـADR مستقل) |
| 6 | Central Audit Trail | Proposed (مبدأ "Auditability by Default" مذكور ضمن Constitution Section 23 كقاعدة، لكن لم يصدر له ADR مستقل بعد) |
| 7 | Configurable Workflow Engine | Proposed |
| 8 | Module SDK and Module Template are required | Proposed |

## New Decisions Accepted via Constitution v1 (لم تكن مدرجة سابقًا كـProposed هنا)

هذه قرارات وردت في موافقة المستخدم الصريحة على Constitution v1 ولم تكن موجودة سابقًا
في هذا الملف بصيغة Proposed — أُضيفت مباشرة كـAccepted مع ADR مقابل:

| # | القرار | ADR |
|---|---|---|
| 9 | Domain-Driven Design كمنهج تصميم | 0002 |
| 10 | Schema per Module | 0003 |
| 11 | Event-Driven Integration (كمبدأ تكامل بين Modules) | 0004 |
| 12 | Hybrid Tenant Isolation | 0005 |
| 13 | Independent Device Integration Gateway | 0006 |
| 14 | Governed AI Gateway مع Human-in-the-Loop إلزامي | 0007 |
| 15 | SaaS First, On-Premise Ready, Hybrid Ready | 0009 |
| 16 | Arabic/English وLocalization من البداية | 0010 |

## ملاحظة

عشرة قرارات فقط أصبحت **Accepted** رسميًا حتى الآن (ADR 0001–0010)، وكلها موثقة في
`docs/constitution/PROJECT-CONSTITUTION.md`. القرارات المتبقية (Event-Driven
Notifications تحديدًا، Central Audit Trail كـADR مستقل، Configurable Workflow
Engine، Module SDK/Template) تبقى **Proposed** ولم تُدرس بعد بصورة مستقلة — لا يجوز
اعتبارها معتمدة ضمنًا لمجرد ارتباطها بمبدأ Accepted أعم. لا يُعدَّل أي قرار Accepted
هنا دون ADR جديد يوثق التغيير (Superseded-by)، حسب القاعدة المذكورة أعلاه في هذا
الملف.

## ملاحظة v2 (2026-07-15 — Constitution Enterprise Upgrade)

ترقية Constitution إلى v2 (Sections 48–62: Engineering Principles, Fitness
Functions, Decision Matrix, Non-Functional Budgets, Quality Gates, Module
Acceptance Checklist, Architecture Radar, Evolution Strategy, Repository/ADR/
Documentation/Glossary Governance, Architecture Review Board, Risk Governance,
Self Validation) **لم تُنتج أي قرار معماري جديد على مستوى ADR** — كل محتوى v2
مبني على القرارات العشرة المعتمدة أعلاه (ADR 0001–0010) دون تغيير أي منها. لذلك
لا صف جديد في جدول ADR Index أعلاه، ولا تغيير في حالة أي قرار Accepted/Proposed
موجود. التفاصيل الكاملة: `docs/constitution/CHANGELOG.md` (قسم v2) و
`docs/constitution/REVIEW-REPORT.md` (v2 Addendum).
