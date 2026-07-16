**Proactive duplicate avoidance, not a reactive resolution.** ERPNext's
Purchase Receipt owns PO/receipt/invoice matching; on confirmation, it
calls OpenBoxes's (Module 18) stock-increase API rather than using
ERPNext's own native stock module — keeping OpenBoxes as the platform's
single stock-ledger Adoption Point (established at Module 18) without
ever creating a 2nd Detected Duplicate. Logged explicitly in
`MASTER_DEPENDENCY_MATRIX.md` as a "designed-in" integration, not a
caught overlap.
