# Architecture Review — HL7 Integration Engine

Mirth's channel/transformer model (receive → transform via JavaScript/
Groovy → route to destination) is purpose-built for exactly this
Feature's job and matches ADR 0006's Anti-Corruption-Layer framing for
Device Integration. Apache Camel offers the same integration-pattern
power generically (Enterprise Integration Patterns) but with none of
Mirth's healthcare-specific tooling (message-type-aware editors, built-in
HL7 ACK handling) — meaning a Camel-based build would re-implement a
meaningful slice of what Mirth already provides out of the box.
