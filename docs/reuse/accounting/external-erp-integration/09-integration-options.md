Confirms the platform-wide integration boundary: every financial event
originating in a platform Bounded Context (Diagnostic Ordering, Result
Verification, Inventory, Procurement) crosses into ERPNext via its REST
API, never duplicating ledger/accounting logic natively.
