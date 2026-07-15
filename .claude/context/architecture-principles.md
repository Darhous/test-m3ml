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

## Principles — Status After Constitution v1

بعد اعتماد `docs/constitution/PROJECT-CONSTITUTION.md` v1 (2026-07-15)، تحوّلت بعض
هذه المبادئ إلى **Accepted** رسميًا (مع ADR مقابل). المبادئ التي لم تُذكر صراحة ضمن
القرارات المعتمدة من المستخدم لهذه الجولة **تبقى Draft** — لم تُفترض ولم تُرتَّب
بالتخمين (وفق قاعدة No-Guessing في `CLAUDE.md`).

| # | Principle | الحالة | Related ADR |
|---|---|---|---|
| 1 | Modular Monolith First | **Accepted** | [0001](../../docs/adr/0001-modular-monolith-first.md) |
| 2 | Selective Service Extraction when justified | **Accepted** | [0001](../../docs/adr/0001-modular-monolith-first.md) |
| 3 | Domain-Driven Design | **Accepted** | [0002](../../docs/adr/0002-domain-driven-design.md) |
| 4 | Clear Bounded Contexts | **Accepted** | [0002](../../docs/adr/0002-domain-driven-design.md) |
| 5 | Backend-Enforced Authorization | **Accepted** | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| 6 | Least Privilege | **Accepted** | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| 7 | Explicit Data Scopes | **Accepted** | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| 8 | Event-Driven Integration | **Accepted** | [0004](../../docs/adr/0004-event-driven-integration.md) |
| 9 | API-First Design | **Accepted** | [0001](../../docs/adr/0001-modular-monolith-first.md) (part of the same Architecture decision block) |
| 10 | Auditability by Default | **Accepted** (as "Full Auditability") | [0008](../../docs/adr/0008-unified-login-and-policy-based-access.md) |
| 11 | Secure by Design | Draft | — (not individually named in the Accepted decision block; covered only indirectly) |
| 12 | Privacy by Design | Draft | — (not individually named in the Accepted decision block) |
| 13 | Human-in-the-Loop for sensitive medical AI actions | **Accepted** | [0007](../../docs/adr/0007-governed-ai-gateway.md) |
| 14 | Avoid Direct Module Coupling | **Accepted** (as "No direct cross-module database access") | [0003](../../docs/adr/0003-schema-per-module.md) |
| 15 | Contracts over implementation sharing | **Accepted** | [0001](../../docs/adr/0001-modular-monolith-first.md) |
| 16 | Configuration over hardcoded workflows | Draft | — |
| 17 | Multi-Tenant Readiness | **Accepted** (as "Multi-Tenant, Multi-Organization, Multi-Branch") | [0005](../../docs/adr/0005-hybrid-tenant-isolation.md), [0009](../../docs/adr/0009-saas-first-on-premise-and-hybrid-ready.md) |
| 18 | Observability by Default | Draft | — |
| 19 | Backward-Compatible Evolution | Draft | — (API Versioning and Compatibility Rules exist as a Constitution structural section, but this principle itself was not individually named Accepted) |

New principles introduced directly by Constitution v1 (not present in the original
19-item Draft list):

| # | Principle | الحالة | Related ADR |
|---|---|---|---|
| 20 | Schema per Module (data ownership) | **Accepted** | [0003](../../docs/adr/0003-schema-per-module.md) |
| 21 | Hybrid Tenant Isolation | **Accepted** | [0005](../../docs/adr/0005-hybrid-tenant-isolation.md) |
| 22 | Independent Device Integration Gateway (Anti-Corruption Layer at device boundary) | **Accepted** | [0006](../../docs/adr/0006-independent-device-gateway.md) |
| 23 | Governed AI Gateway (independent, auditable, Human-in-the-Loop) | **Accepted** | [0007](../../docs/adr/0007-governed-ai-gateway.md) |
| 24 | SaaS First / On-Premise Ready / Hybrid Ready, replaceable cloud provider | **Accepted** | [0009](../../docs/adr/0009-saas-first-on-premise-and-hybrid-ready.md) |
| 25 | Arabic/English + RTL/LTR + Multi-Currency + Multi-Timezone from v1 | **Accepted** | [0010](../../docs/adr/0010-arabic-english-and-localization-first.md) |

## ملاحظة

القائمة **لم تُعاد ترتيبها ولم يُحذف أي بند سابق** — كل بند احتفظ برقمه وحالته
التاريخية، وأُضيف عمود "Related ADR" فقط لمن أصبح Accepted. البنود التي بقيت Draft
(11, 12, 16, 18, 19) تبقى كذلك لأنها لم تُذكر صراحةً ضمن قرارات هذه الجولة — لا
يجوز اعتبارها معتمدة ضمنًا. أي تعارض محتمل بين مبدأ Accepted ومبدأ آخر ما زال Draft
يُحل لصالح النص الصريح في `docs/constitution/PROJECT-CONSTITUTION.md`، لا بالتخمين
هنا.
