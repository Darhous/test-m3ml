# AGPL Legal Checklist

**Confirmed: legal review before production remains MANDATORY for every
item below.** This Board does not waive, downgrade, or silently resolve
any AGPL-3.0 finding from the reuse program — that would exceed this
Board's authority (formal legal review requires counsel, not an
architecture board's judgment call).

## Why AGPL-3.0 Specifically

AGPL-3.0's distinguishing clause (Section 13) extends the GPL's
copyleft obligation to **network use**: if a user interacts with an
AGPL-licensed program over a network (e.g., a SaaS product built on it),
the operator must offer that user the corresponding source, including
any modifications — even without traditional "distribution." This is
architecturally significant for a multi-tenant SaaS platform (ADR-0009)
in a way it would not be for an internally-distributed desktop tool.

## Checklist — Adopted, Running AGPL-3.0 Engines (5)

| # | Engine | Module | Obligation Trigger | Commercial Escape Hatch? | Action Required Before Production |
|---|---|---|---|---|---|
| 1 | Cal.com | Scheduling and Encounters | Network use (multi-tenant SaaS booking) | Yes — Cal.com offers a commercial license | [ ] Legal counsel determines: (a) rely on AGPL compliance (offer modified source to users), or (b) purchase commercial license. Cal.diy (MIT fork) remains a documented fallback if neither is acceptable. |
| 2 | Atlas CMMS | Asset and Maintenance | Network use | Yes — dual-licensed, commercial tier available | [ ] Same determination as above. openMAINT (also AGPL) is not a license-clean fallback — if Atlas CMMS is legally blocked, re-open this decision rather than assuming openMAINT solves it. |
| 3 | openIMIS | Insurance and Corporate Contracts | Network use | **Not confirmed** — this Board did not find evidence of a commercial-license alternative for openIMIS in the reuse program's research | [ ] Legal counsel determines AGPL compliance approach. **No commercial escape hatch identified** — if AGPL compliance is unacceptable, this Feature may require re-opening Build-vs-Buy analysis, not a simple swap. |
| 4 | Frappe Helpdesk | CRM and Support | Network use | Not confirmed this pass | [ ] Legal counsel review. **License-drift note**: do not assume the same compliance posture as ERPNext/Frappe HR (GPL-3.0) — this is a separately-licensed product. |
| 5 | Frappe CRM | CRM and Support | Network use | Not confirmed this pass | [ ] Legal counsel review. Same license-drift note as Frappe Helpdesk. |

## Checklist — Unconfirmed-License Engines (Equal Urgency, 2)

These are not confirmed AGPL, but were never confirmed *anything* —
treated with the same mandatory-verification urgency because "unknown"
carries the same practical blocker as "known-conditional" until
resolved.

| # | Engine | Module | Action Required Before Production |
|---|---|---|---|
| 6 | Novu | Notification Service (+ 3 other Modules) | [ ] Read the actual current license text at `github.com/novuhq/novu`'s LICENSE file. If AGPL or a similar network-use copyleft, add to the numbered list above. |
| 7 | Documenso | Document Management | [ ] Read the actual current license text. **Priority: elevated** — this Feature is Sensitive-Operation-adjacent (e-signature/consent capture), so an unresolved license question sits closer to a compliance-critical path than Novu's. |

## Checklist — Reference-Only (No Running Code, Informational)

| Engine | Note |
|---|---|
| OpenELIS Global | AGPL-3.0, but explicitly **not adopted as a running dependency** — used only as a FHIR-native architecture Reference (`laboratory-execution/worklist-management`). No platform code links against or deploys OpenELIS Global. **No legal action required**, but flagged here so a future reviewer does not mistake its presence in `MASTER_LICENSE_MATRIX.md` for an active obligation. |

## Checklist — One LGPL-3.0 Verification (Lower Urgency, Included for Completeness)

| Engine | Module | Action Required |
|---|---|---|
| Alfresco Community Edition | Document Management | [ ] Independently confirm the LGPL-3.0 license string (currently carried forward as "unverified this pass" from the reuse program). LGPL's library-level copyleft is lower-risk than AGPL's network-use clause, but the string itself was never actually read. |

## Board Recommendation

1. **Schedule a formal legal review as an explicit, tracked early SAD-
   phase workstream** covering items 1-7 above — not an implicit
   assumption that "someone will get to it."
2. **Prioritize items 3-5 and 7** (no confirmed commercial escape hatch,
   or Sensitive-Operation-adjacent) over items 1-2, 6 (a documented
   commercial alternative exists, lowering the urgency of a fast legal
   answer).
3. **Do not begin production deployment of any of the 7 checklist items
   above until its row is checked off** by actual legal counsel, not by
   this Board's architectural judgment.
4. This checklist is the direct, unmodified carry-forward of
   `MASTER_READINESS_REPORT.md` Section 3 and `MASTER_LICENSE_MATRIX.md`'s
   closing note — re-verified, not re-derived, per this phase's scope
   discipline.
