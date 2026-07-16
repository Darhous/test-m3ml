ERPNext's Buying module integrates with `supplier-rfq` (this Module) as
its own native RFQ step, and with `receiving-goods` (this Module) for
PO-to-receipt matching, which itself integrates with OpenBoxes
(Module 18) for the actual stock increase — an explicit 3-system chain
(ERPNext PO → receiving-goods matching → OpenBoxes stock), documented to
avoid the kind of unflagged overlap Module 17/18 caught and resolved.
Approval-workflow notifications reuse Novu (Module 5).
