# Architecture Review — WhatsApp Integration

Novu's provider abstraction means a specific BSP (Twilio vs. 360dialog
vs. direct Meta) can be swapped via configuration, not code — the
platform should not hard-code a single BSP dependency, per this
program's own vendor-independence discipline.
