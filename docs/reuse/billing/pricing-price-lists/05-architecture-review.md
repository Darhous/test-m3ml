ERPNext's Pricing Rule engine applies tiered/conditional discounts at
invoice-generation time. Module 12's `order-catalog-pricing` already
established the platform-owned pricing model for diagnostic-order
catalog pricing specifically (correctly BUILD, per that Feature's
Core-Domain-adjacent reasoning) — this Feature's ERPNext Pricing Rules
apply at the commercial/invoice layer on top of that catalog price,
not a duplicate but a distinct layer (list price vs. applied discount).
