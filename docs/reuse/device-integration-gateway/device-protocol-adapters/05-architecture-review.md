# Architecture Review — Device Protocol Adapters

Each Vendor-API adapter is an Anti-Corruption Layer instance within the
Gateway (ADR 0006), normalizing to the same platform Domain Event
vocabulary as HL7/ASTM sources — one consistent output shape regardless
of input protocol diversity.
