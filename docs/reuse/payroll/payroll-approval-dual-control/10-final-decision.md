**Final Decision: ENGINE + ADAPTER (shared OPA) + BUILD**

7th confirmed OPA reuse. The dual-control workflow itself is platform-
owned, but its authorization decision is centrally enforced via the
same policy engine backing every other Sensitive Operation in the
platform.

**Module 26 summary:** Payroll's 2 Features cleanly split between the
program's 2 most-reused Engines: Frappe HR (Module 25's sibling
adoption) for calculation, OPA (Module 1) for the sensitive-operation
approval gate — no new research needed for either.
