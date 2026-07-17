# Master SDK Catalog

Candidates classified as an **SDK** (a client/integration kit for an
external service, e.g., a payment gateway SDK, a WhatsApp Business API
SDK) across all Modules.

| Module | Feature | SDK | Vendor/Service It Wraps | Vendor Independence Note |
|---|---|---|---|---|
| Notification Service | whatsapp-integration | Novu's native WhatsApp provider (BSP vendor TBD) | WhatsApp Business Platform | BSP selection is a commercial decision, not a software Build-vs-Buy one |
| Payments and Treasury | payment-gateway-abstraction | Platform-owned per-gateway adapters (Fawry, Paymob, international processors) | Fawry, Paymob (commercial vendors, not OSS) | Omnipay's adapter-pattern architecture logged as a design Reference only; BUILD, not a 3rd-party SDK dependency |
| SaaS Commercial Operations | saas-billing | Kill Bill's payment-plugin architecture (Stripe/Adyen/GoCardless plugins, or a custom Fawry/Paymob plugin) | Payment processors | May reuse `payment-gateway-abstraction`'s Egypt-specific adapters via a custom Kill Bill plugin rather than a 3rd payment-integration layer |

**Program note:** genuine third-party SDK adoptions were rare in this
program — most external-service integration needs resolved to either a
full Engine (Novu, Kill Bill), a platform-owned per-vendor adapter
(payment gateways, device protocols — Module 4's `device-protocol-
adapters` precedent), or a Vendor/commercial decision explicitly outside
Build-vs-Buy scope (Fawry, Paymob, WhatsApp BSPs).
