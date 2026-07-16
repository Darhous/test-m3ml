# Global Search Log — Patient Registry / MPI

**Query:** `OpenMRS vs HAPI FHIR Patient resource open source patient
registry MPI 2026 healthcare`

**Finding:** Two distinct categories. **OpenMRS** — a full open-source
EMR platform (MPL 2.0), globally mature, huge adoption in resource-
constrained health systems, has its own FHIR module and MPI
integrations. **HAPI FHIR** — a FHIR server/API implementation with a
native MDM (Master Data Management) module for patient matching/
blocking rules. **OpenCR** (Open Client Registry) — a dedicated Master
Patient Index/Client Registry implementation, explicitly cited as
integrable with OpenMRS's own MPI module.

**Critical scoping decision:** adopting OpenMRS wholesale would mean
replacing this platform's own Core Domain (ADR-0011 Amended,
"Patient-to-Result Orchestration") with an external system's patient/
clinical model — directly contradicting Wave 7's finding that deepest
modeling investment belongs in this platform's own Core Domain, not an
adopted system. OpenMRS is therefore evaluated and **not selected**, not
overlooked.
