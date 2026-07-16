No new search — ERPNext's Purchase Receipt doctype (found during
`purchase-requisition-order`'s search) natively performs PO-to-receipt
matching. Whether this should trigger OpenBoxes's stock ledger directly,
or whether ERPNext's own stock module should be used instead (risking a
duplicate of Module 18's `stock-management`), is explicitly addressed in
`09-integration-options.md` — not left as an unflagged overlap.
