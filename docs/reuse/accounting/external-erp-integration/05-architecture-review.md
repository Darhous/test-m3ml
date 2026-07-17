The "Integration" architecture is already fully realized: the platform's
own Aggregates (orders, results, patients) never duplicate financial
logic — they emit events/API calls into ERPNext (already the single
Adoption Point across Procurement, Supplier Management, Billing,
Payments and Treasury, and this Module), which owns the full financial
system of record. This is the clean Bounded-Context-respecting
integration model Wave 3 was gesturing toward.
