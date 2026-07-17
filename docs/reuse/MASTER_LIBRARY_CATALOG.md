# Master Library Catalog

Candidates classified as a **Library** (linked into the platform's own
codebase, not a separately-deployed service) across all Modules.

| Module | Feature | Library | Language/Ecosystem | Why Library, Not Engine |
|---|---|---|---|---|
| Scheduling and Encounters | resource-calendar | FullCalendar | JavaScript/TypeScript | Calendar-rendering component linked into the platform UI, not a separately-deployed service |
| Analytics | forecasting-engine | Prophet | Python | Statistical forecasting library invoked in-process, no independent deployment footprint |
| Specimen Operations | barcode-labeling | ZXing (or equivalent) | Java/multi-platform port | Barcode encode/decode routine linked into capture flow, not a service |
| AI Operations Gateway | semantic-search | pgvector | PostgreSQL extension | Reuses the platform's existing PostgreSQL, no dedicated vector-DB service needed |
| Inventory | barcode-scanning | ZXing (reused) | Java/multi-platform port | 2nd Module reusing the same decode library as Specimen Operations |
| Result Verification and Reporting | clinical-report-generation | Deferred — specific candidate (e.g. JasperReports/Carbone/pdfmake) not selected | Stack-dependent | Genuinely premature to pick before the SAD fixes the platform's frontend/backend stack; not guessed |

**Program complete.** Libraries are intentionally the smallest category
in this program — most capability needs resolved to a full Engine
(reusable across many Features) rather than a linked-in Library, which
is itself evidence for the "reuse mature software" directive: Engines
carry more of the hard problem (state management, workflow, persistence)
than a Library typically does.
