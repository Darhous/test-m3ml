# Architecture Review — ASTM Integration

Same channel-model fit as HL7. ASTM's serial/low-level framing (STX/ETX,
checksums) is more custom-parsing-heavy than HL7's message structure —
whichever core engine is chosen, this sub-protocol will likely need more
platform-specific glue than HL7 does.
