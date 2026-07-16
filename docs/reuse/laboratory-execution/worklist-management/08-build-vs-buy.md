This is the program's most deliberately-weighed Build-vs-Buy call.
Arguments considered on both sides:

**For adopting SENAITE or OpenELIS Global wholesale (ENGINE + ADAPTER):**
Both are mature, feature-complete, production-proven LIMS engines with
built-in worklist, QC, and calibration modules — adopting one would
plausibly save the single largest number of engineering hours of any
Feature in the program (a full Laboratory Execution engine is a
multi-year build from scratch). This is exactly the kind of case the
mission's "if it can save 1000 hours, reuse it" directive is aimed at.

**Against wholesale adoption:** Both are complete, opinionated
system-of-record applications — not embeddable engines with a clean
adapter seam. Adopting either would mean running a second, parallel
Order/Specimen/Result system-of-record alongside the platform's own,
directly displacing ADR-0011 Amended's Core Domain ("Patient-to-Result
Orchestration") for the single Feature architecturally closest to it —
the same reasoning that correctly rejected OpenMRS (Module 9), Bahmni
(Module 12), and OpenELIS/Bahmni wholesale (Module 12-13), applied with
even more force here since Laboratory Execution sits in the middle of
that exact orchestration chain, not adjacent to it.

**Resolution:** REFERENCE + BUILD, consistent with Modules 9, 10, 12, 13
— not a pattern-reuse shortcut, but the same principle reaffirmed after
genuine reconsideration of the wholesale-adoption alternative, which was
taken seriously and rejected on Core Domain grounds, not dismissed
out of hand. OpenELIS Global is the primary Reference source (FHIR-native
data shapes, matching 6 prior Modules' convention); SENAITE is a
secondary Reference specifically for its mature Westgard-rules QC-module
design, reused in `quality-control-tracking` below.
