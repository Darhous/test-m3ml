| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Running ERPNext (procurement) alongside OpenBoxes (inventory) as 2 separate systems creates integration overhead vs. a single unified ERP | Medium | Medium | Explicit API-level integration contract at SAD time (PO → receiving-goods → OpenBoxes stock), same discipline as the Module 17/18 duplicate resolution |
| GPL-3.0 self-hosted use is clear, but any future decision to distribute modified ERPNext code externally would need re-review | Low | Low | Flagged for awareness, not currently a blocker |
