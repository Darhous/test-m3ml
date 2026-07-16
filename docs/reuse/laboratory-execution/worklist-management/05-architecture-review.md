**SENAITE**: Plone/Zope CMS-based, Python. Content-object-oriented
architecture (Archetypes/Dexterity), RESTful JSON API layer added on top.
Powerful and mature for its own ecosystem, but the underlying CMS
paradigm is a poor architectural fit for a modern modular-monolith
platform (Constraint: no forced microservices, but also no adoption of a
foreign 20-year-old CMS core as a platform module) — integrating it
as anything other than a separately-run, loosely-coupled system would
mean absorbing Plone's entire object database and templating model.

**OpenELIS Global**: Java/Spring backend + React/Carbon Design System
frontend, FHIR R4-native data model. Materially closer to a
conventional modern service architecture, and its FHIR-native design
means its worklist/QC/calibration data shapes are expressed in the same
resource vocabulary (`ServiceRequest`, `Task`, `Specimen`,
`DiagnosticReport`) the platform has already adopted as Reference
patterns in 6 prior Modules (9,10,11,12,13, and implicitly this one) —
architecturally, it is the stronger Reference source of the two.

**Neither is proposed as a directly-embedded Engine.** Both are complete,
opinionated, whole-system LIMS applications with their own UI, auth, and
data ownership model — adopting either as an ENGINE + ADAPTER would mean
running a second, largely-redundant system-of-record for exactly the
Aggregates (Order, Specimen, Result) ADR-0011 Amended already assigns to
the platform's own Core Domain. See `10-final-decision.md`.
