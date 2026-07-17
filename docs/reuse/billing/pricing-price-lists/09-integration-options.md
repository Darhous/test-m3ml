Reads base list price from Module 12's `order-catalog-pricing`
Aggregate; applies ERPNext Pricing Rules on top at invoice time via
`invoicing-engine`. Explicit layering documented to prevent a future
Detected Duplicate finding, the same proactive-avoidance discipline as
Module 19's `receiving-goods`.
