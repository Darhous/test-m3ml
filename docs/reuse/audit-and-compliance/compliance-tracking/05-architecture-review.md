# Architecture Review — Compliance Tracking

All 3 candidates are **internal, operator-facing governance tools**
(used by the platform's own Compliance Officer/Auditor personas, Wave 2)
— not something patients, doctors, or tenant end-users interact with.
This means adopting one carries far lower architectural integration risk
than a Feature embedded in the clinical workflow: it can run as a
largely standalone internal tool, cross-referencing (not tightly
coupling to) the Risk Register/Assumption Register/Open Questions
Register concepts this Discovery program itself already uses. None of
the 3 is purpose-built for healthcare-specific regulatory tracking
(Egypt's ETA/PDPL/EDA/UHI), so meaningful configuration/customization
work should be expected regardless of which is chosen.
