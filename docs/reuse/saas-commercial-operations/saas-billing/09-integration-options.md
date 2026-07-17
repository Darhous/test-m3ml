Consumes `subscription-plan-management` and `usage-metering-
entitlements` (this Module); may reuse `payment-gateway-abstraction`'s
(Module 22) Egypt-specific gateway adapters via a custom Kill Bill
payment plugin, avoiding a 3rd payment-integration layer. Logged in
`MASTER_DEPENDENCY_MATRIX.md` distinguishing this Feature from Module
21's `invoicing-engine` explicitly.
