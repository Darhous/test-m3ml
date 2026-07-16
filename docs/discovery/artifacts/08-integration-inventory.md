# Integration Inventory (Discovery, Phase 08)

**Status: Draft — Assumption-Driven Autonomous Run.** Covers every external
boundary identified in Phase 06's Context Map. No vendor/product is named
anywhere — only protocol/integration *categories*, most already anticipated
by Constitution Section 24's readiness list (Accepted, not invented here).

## Device Integration — Lab Analyzer Device

| Field | Value |
|---|---|
| Protocol category candidates | HL7 v2, ASTM, Vendor API (all already on Constitution Section 24's readiness list) |
| Data imported | Raw result values → `ProvenanceInfo` (device ID, adapter, timestamp, raw-payload reference) |
| Context Mapping pattern | Anti-Corruption Layer (consumer side, Test Processing) / Open Host Service (provider side, Device Gateway) — confirmed from Phase 06 |
| Failure mode (first pass) | Connectivity loss, malformed message, duplicate message. Per Constitution Section 24: isolated, logged, surfaced for review — never allowed to write partial/invalid state into `TestResult`. Proposed: failed imports land in a review queue, matching the Constitution's own illustrative Device Gateway diagram (Section 24). |
| Resolves Phase 07 #21 (processing-failure recovery) — partially | A device-side import failure is distinct from an in-lab `TestProcessingFailed` event (Phase 07) — this phase clarifies the device-import failure path specifically; the *retry/escalation policy value* is still Open. |

## Device Integration — Portable Collection Device (home visits)

| Field | Value |
|---|---|
| Protocol category candidates | Vendor API (real-time), File-Based (batch sync) |
| Data imported | `SpecimenCollectedAtHome` confirmation, collection metadata |
| Context Mapping pattern | Anti-Corruption Layer / Open Host Service, same as above |
| Failure mode (first pass) | Sync delay or full offline operation during a home visit. |
| Resolves H6 (offline mode) — at a design-pattern level only | Proposed pattern: local-first capture (collector device records `SpecimenCollectedAtHome` locally) with eventual sync to the platform once connectivity returns. **This does not answer whether Offline Mode is actually required** (`open-questions.md` #6 stays Open) — it only shows a pattern that would satisfy it if confirmed. |
| Resolves Phase 07 #22 (home-visit retry policy) — partially | Establishes that "failure" here is really "sync delay," not necessarily a failed visit — the *actual* failed-visit (no-show) retry policy (H4) remains Open, distinct from a sync delay. |

## Device Integration — Chain-of-Custody Design (resolves H5, design-level only)

**Proposed shape for `ChainOfCustodyRecord`** (Phase 05's candidate Value
Object): an ordered sequence of handoff entries, each with `{handoffFrom,
handoffTo, timestamp, confirmationMethod}` — e.g., Collector→Transport,
Transport→Lab Accessioning. **This is a design proposal, not a confirmed
requirement** — the platform's actual chain-of-custody/regulatory
requirement is still unconfirmed.

## External API Partner — Insurance/Payer System

| Field | Value |
|---|---|
| Direction | Outbound (`ClaimSubmitted`), Inbound (`ClaimAdjudicated`/`ClaimDenied`) |
| Data exchanged | Claim details, eligibility, adjudication result |
| Context Mapping pattern | **Anti-Corruption Layer + Conformist** — the platform likely must conform to the payer's claim format for submission (a payer rarely adapts to an individual platform), while still translating their response into internal `Claim` state via ACL rather than exposing their raw format to the rest of Billing and Claims. |
| Failure mode (first pass) | Payer system unreachable, malformed/delayed adjudication response, response referencing an unknown claim ID. |
| Gating factor | Entire integration remains provisional pending `open-questions.md` #17 (billing/insurance model) — the least confident integration in this inventory. |

## Legacy System Integration

**No profile discoverable.** `open-questions.md` #13 (legacy migration
needs) has zero Confirmed or even Inferred basis — no legacy system type,
data format, or migration scope is stated anywhere in this project's
context. Per the No-Guessing Rule, **nothing is invented here** — this
integration category remains an empty placeholder pending real input.

## Notification Channels (candidates, resolves part of `open-questions.md` #10)

| Candidate Channel | Basis | Confidence |
|---|---|---|
| SMS | Common patient-convenience channel in healthcare/lab industry | Inferred — Industry Reference, Medium |
| Push (mobile app) | Implied by `vision.md`'s Patient App client surface | Inferred — Extrapolated, Medium |
| Email | Common professional channel for Doctor-facing notifications | Inferred — Industry Reference, Medium |
| In-Portal notification | Implied directly by `vision.md`'s Portal/Dashboard routing (Confirmed) | Inferred — Extrapolated, Medium-High |
| WhatsApp / other messaging | Mentioned as a candidate in the original open-questions.md #10 wording itself | Inferred — Industry Reference (regionally common), Low-Medium |

**None of these are Confirmed** — `open-questions.md` #10 remains Open;
this table only narrows the candidate set with reasoning, per
`EXECUTION-GUIDE.md` Section 8 ("narrowed, still Open").

## First-Pass STRIDE Sweep (per integration)

| Integration | Threat Category | First-Pass Note |
|---|---|---|
| Lab Analyzer Device | Spoofing | An unauthenticated device connection could allow a spoofed device to inject fake results — candidate mitigation: device identity/authentication at the Gateway. |
| Lab Analyzer Device | Tampering | Malformed/altered messages — candidate mitigation: message validation before `DeviceImportRecord` creation. |
| Portable Collection Device | Information Disclosure | A lost/stolen field device could expose locally-cached specimen/patient data — candidate mitigation: local data minimization + encryption category (no specific tech named). |
| Insurance/Payer System | Spoofing | A fake adjudication response could falsely mark a claim Approved/Denied — candidate mitigation: mutual authentication with the payer, response signature verification category. |
| Insurance/Payer System | Repudiation | No proof of claim submission/response — candidate mitigation: full audit logging of the exchange (Constitution Section 23 already requires this for the platform side). |
| Notification Channels | Information Disclosure | Sensitive result content leaking via an insecure channel — already governed by Constitution Section 26; reaffirmed here as directly relevant to every candidate channel above. |

**Full STRIDE + mitigation mapping is Phase 11's job** — this pass exists
so integration *design* doesn't ignore obvious threats from day one, per
Playbook 08's own scope.
