ERPNext's Purchase Receipt performs the PO/receipt match and quantity/
quality verification step; the resulting confirmed-receipt event calls
OpenBoxes's stock-increase API rather than using ERPNext's own built-in
stock module — deliberately avoiding a 2nd parallel stock ledger, the
same discipline that resolved the Module 17/18 duplicate.
