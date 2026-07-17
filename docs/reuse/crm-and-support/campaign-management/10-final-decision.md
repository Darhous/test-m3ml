**Final Decision: BUILD (campaign logic) + ENGINE + ADAPTER (composed:
Frappe CRM + Novu)**

No dedicated marketing-automation product independently verified this
pass; the composition of already-adopted Frappe CRM and Novu (4th
confirmed reuse) is the evidence-based answer rather than introducing an
unverified new dependency.

**Module 27 summary:** `helpdesk-ticketing` and `call-center-crm` adopt
Frappe Helpdesk/CRM (same-vendor-family, AGPL-3.0 — explicitly flagged
as a license-drift finding distinct from ERPNext/HR's GPL-3.0);
`complaint-feedback-management` reuses Frappe Helpdesk with an explicit
escalation path to Module 16's platform-owned CAPA system;
`campaign-management` composes existing Engines rather than introducing
a new one.
