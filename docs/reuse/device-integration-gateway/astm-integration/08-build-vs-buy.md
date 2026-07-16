# Build vs. Buy — ASTM Integration

Follows `../hl7-integration-engine/`'s decision for the base engine; the
ASTM layer itself leans more BUILD (custom parsing) than HL7 regardless
of which core engine is chosen, since neither Mirth-core nor Camel has
strong native ASTM support.
