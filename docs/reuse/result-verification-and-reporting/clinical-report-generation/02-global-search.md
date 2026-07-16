WebSearch performed this pass ("open source clinical lab report
generation PDF template engine HL7 FHIR DiagnosticReport"): confirms FHIR
`DiagnosticReport` supports a formatted-report attachment (e.g., a PDF)
alongside structured data, but the search surfaced only the FHIR
specification itself — no dedicated, actively-maintained open-source
"clinical report renderer" product distinct from a general-purpose PDF/
document-templating library was found. Generic PDF-generation libraries
(e.g., JasperReports, Carbone, pdfmake) exist as a broad category but are
not healthcare-specific and were not independently re-evaluated
candidate-by-candidate this pass — flagged for implementation-time
comparison rather than asserted here.
