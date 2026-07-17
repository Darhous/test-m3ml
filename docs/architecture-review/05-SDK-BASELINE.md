# SDK Baseline — Detailed Validation

## Finding: Zero SDKs Ratified

`MASTER_SDK_CATALOG.md` closes with an explicit program-level note:
*"genuine third-party SDK adoptions were rare in this program — most
external-service integration needs resolved to either a full Engine
..., a platform-owned per-vendor adapter ..., or a Vendor/commercial
decision explicitly outside Build-vs-Buy scope."* This Board re-verifies
that finding rather than manufacturing an SDK category to satisfy the
template.

## Items Considered and Their Actual Classification

| Candidate | Where It Appeared | Why It Is NOT an SDK in this Baseline |
|---|---|---|
| WhatsApp Business Platform integration (BSP, vendor TBD) | Notification Service, `whatsapp-integration` | Delivered through Novu's native WhatsApp provider (an Engine feature), not a standalone SDK the platform integrates directly. BSP vendor selection is a **commercial decision**, not a Build-vs-Buy software one (`MASTER_DECISION_REGISTER.md` row 25). |
| Fawry / Paymob payment gateways | Payments and Treasury, `payment-gateway-abstraction` | Both are commercial vendor APIs, not open-source SDKs. The actual software artifact is a **platform-owned BUILD** (per-gateway adapters), with Omnipay logged only as an architecture Reference, not an adopted dependency (`MASTER_DECISION_REGISTER.md` row 84). |
| Kill Bill payment plugins (Stripe/Adyen/GoCardless, or a custom Fawry/Paymob plugin) | SaaS Commercial Operations, `saas-billing` | Part of the Kill Bill Engine's own plugin architecture, not an independently-adopted SDK. |

## Board Findings

- **0 SDKs ratified — this is a confirmed absence, not an oversight.**
  The category exists in the Baseline template for completeness and
  future use (a genuine SDK need may arise during SAD or Module
  implementation, e.g. a specific payment processor's official client
  library once Fawry/Paymob integration is scoped).
- **No action required of this Board.** Future SDK adoptions (e.g. once
  a specific Fawry/Paymob client library is chosen at implementation
  time) will need their own lightweight review — this Baseline
  establishes the review *pattern* (license, maintenance, vendor
  lock-in) to apply when that happens, not a pre-approved list.
