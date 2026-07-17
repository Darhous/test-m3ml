Kill Bill generates recurring invoices from `subscription-plan-
management`'s plan/subscription state and `usage-metering-entitlements`'
usage data, orchestrating payment collection via its payment-plugin
architecture (Stripe, Adyen, GoCardless, or the platform's own
`payment-gateway-abstraction`, Module 22, if Egypt-specific gateways
like Fawry/Paymob need a custom Kill Bill payment plugin). Explicitly
a separate financial flow from ERPNext's patient/client billing
(Module 21) — 2 Engines, 2 clearly-scoped revenue domains, logged to
prevent a false-positive duplicate flag.
