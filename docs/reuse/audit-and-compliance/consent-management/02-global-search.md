# Global Search Log — Consent Management

## Query Run

`open source consent management platform GDPR HIPAA 2026 vs open source
GRC compliance tracking tool`

## Critical Finding: Category Mismatch

Every credible open-source "Consent Management Platform" found (Klaro,
Osano-class commercial tools, UniConsent) is designed for **website/
cookie/marketing consent** (the ePrivacy/GDPR cookie-banner use case) —
explicitly **not** a substitute for clinical patient-data consent
tracking. One search result states this distinction directly: "Consent
management platforms handle the public-facing consent layer on your
website but are not a substitute for internal HIPAA compliance programs,
BAAs, or data governance tools." This is a real, evidence-based finding,
not an assumption — reported honestly rather than forcing Klaro into a
role it was not designed for.

## Implication

This Feature splits in two:
1. **Website/marketing cookie consent** (relevant to the CRM and Support
   Module's future public-facing pages, not to clinical data) — Klaro is
   a credible candidate, but scoped to CRM Module, not this one.
2. **Clinical/patient data consent** (this Feature's actual Discovery-
   scoped need, Constitution Section 22) — no dedicated open-source
   product was found. The closest structural reference is the **HL7 FHIR
   `Consent` resource** (a data-model standard, not a deployable
   product), already touched on tangentially via Wave 3's FHIR-adjacent
   findings elsewhere in this program.
