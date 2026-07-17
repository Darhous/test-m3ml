A refund request calls the originating gateway adapter's refund API
(`payment-gateway-abstraction`), then records the reversal as an ERPNext
Credit Note against the original Sales Invoice (`invoicing-engine`,
Module 21) — a 2-step composed flow, not a new Engine.
