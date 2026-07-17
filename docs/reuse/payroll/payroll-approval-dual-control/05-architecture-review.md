A payroll run computed by `payroll-calculation-engine` (this Module,
Frappe HR) requires a 2nd, independent approver before disbursement —
enforced via an OPA policy decision (the same decision-with-trace
pattern established at Module 1), not by Frappe HR's own approval
workflow alone, ensuring the dual-control requirement is centrally and
consistently enforced across the platform rather than per-Engine.
