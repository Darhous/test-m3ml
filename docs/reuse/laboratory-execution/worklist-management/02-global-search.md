Live WebSearch performed this pass (not pattern-reuse shorthand, per the
user's explicit instruction that this Module deserves real research):

- "SENAITE LIMS 2026 license architecture" — confirms SENAITE.CORE is
  GPL-2.0, built on Plone/Zope CMS (Python), modular add-on architecture,
  RESTful JSON API, actively maintained, Docker deployment since 3.x.
- "OpenELIS Global LIMS 2026 license architecture production deployment"
  — confirms AGPL-3.0, FHIR R4-native, Carbon Design System (React) UI,
  used at national scale in public-health reference labs, offline/
  air-gapped deployment support.
- "SENAITE vs OpenELIS Global comparison 2026" — both fee-free,
  consultancy-supported; no CNCF/foundation governance for either
  (neither is foundation-graduated, unlike OPA/Keycloak).
- "Westgard rules quality control open source LIMS module" — confirms QC/
  calibration functionality is a bundled module inside full LIMS products,
  not available as an independent open-source component — relevant to
  `quality-control-tracking` and `calibration-tracking` below.

No new candidate beyond SENAITE and OpenELIS Global (already identified
in Modules 12-13) was found as a credible, actively-maintained, full
Laboratory Execution engine. Bahmni (Module 12) is OpenMRS+OpenELIS-based,
not independent for this Feature.
