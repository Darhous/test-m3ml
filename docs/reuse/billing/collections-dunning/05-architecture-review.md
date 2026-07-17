ERPNext's Dunning document is created against an overdue Sales Invoice,
pre-filled from a configurable Dunning Type (interest/fees/text blocks);
payment resolution creates a Payment Entry recording interest/fees as
Payment Deductions. Reminder sequences (overdue dates, partial payments,
unviewed invoices) can route through Novu (Module 5) instead of
ERPNext's native email, for platform-wide notification consistency.
