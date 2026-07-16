# Security Review — HL7 Integration Engine

Mirth 4.5.2 being frozen is itself the security finding: any CVE
discovered in the engine after the OSS freeze will not receive an
official free patch. This is a **material, ongoing security risk**, not
a one-time adoption cost — logged as the top risk in `12-risk-analysis.md`.
Apache Camel, being actively maintained, does not carry this specific
risk but shifts security responsibility onto the platform's own
integration code instead.
