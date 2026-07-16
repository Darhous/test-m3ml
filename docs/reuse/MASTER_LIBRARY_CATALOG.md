# Master Library Catalog

Candidates classified as a **Library** (linked into the platform's own
codebase, not a separately-deployed service) across all Modules.

| Module | Feature | Library | Language/Ecosystem | Why Library, Not Engine |
|---|---|---|---|---|
| Scheduling and Encounters | resource-calendar | FullCalendar | JavaScript/TypeScript | Calendar-rendering component linked into the platform UI, not a separately-deployed service |
| Analytics | forecasting-engine | Prophet | Python | Statistical forecasting library invoked in-process, no independent deployment footprint |
| Specimen Operations | barcode-labeling | ZXing (or equivalent) | Java/multi-platform port | Barcode encode/decode routine linked into capture flow, not a service |
