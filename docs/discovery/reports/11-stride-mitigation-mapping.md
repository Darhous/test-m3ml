# Full STRIDE and Mitigation Mapping (Discovery, Phase 11)

Completes the first-pass STRIDE notes from Phase 08 (integrations) and
Phase 10 (AI use cases) into full 6-category coverage with mitigation
categories and named owners, per Constitution Section 37.

## Integration Surfaces

### Lab Analyzer Device

| STRIDE | Threat | Mitigation Category | Owner |
|---|---|---|---|
| Spoofing | Fake device injects fabricated results | Device identity/mutual authentication at the Gateway | Device Integration Gateway (candidate Module) |
| Tampering | Message altered in transit | Message integrity check before `DeviceImportRecord` creation | Device Integration Gateway |
| Repudiation | No proof of what a device actually sent | Full audit of raw payload + provenance (already Required, Constitution Section 24) | Device Integration Gateway |
| Information Disclosure | Result data intercepted in transit | Encrypted-transport category | Device Integration Gateway |
| **Denial of Service** | Device floods Gateway with malformed messages | Rate limiting / circuit-breaker category | **Architecture Review Board** — accepted risk, no platform-wide policy yet (pre-existing gap, `docs/constitution/REVIEW-REPORT.md` Open Risk R1) |
| Elevation of Privilege | Malformed message exploits parser for broader access | Strict input validation / sandboxed parsing | Device Integration Gateway |

### Portable Collection Device

Same 6 categories as Lab Analyzer Device, with Information Disclosure
elevated: a lost/stolen field device could expose locally-cached specimen/
patient data (local-first capture pattern, Phase 08) — mitigation category:
local data minimization + encryption-at-rest category, owner: Device
Integration Gateway.

### Insurance / Payer System

| STRIDE | Threat | Mitigation Category | Owner |
|---|---|---|---|
| Spoofing | Fake adjudication response falsely marks a claim Approved/Denied | Mutual authentication with the payer | Billing and Claims Module (candidate) |
| Tampering | Claim data altered in transit | Message integrity / transport security category | Billing and Claims Module |
| Repudiation | No proof of submission/response | Full audit logging of the exchange (Constitution Section 23) | Billing and Claims Module |
| Information Disclosure | Financial + PII data exposure | Encryption + data minimization category | Billing and Claims Module |
| Denial of Service | Payer system unavailable | Graceful degradation (Constitution Section 34, already Accepted) applied to this integration specifically | Billing and Claims Module |
| Elevation of Privilege | Compromised payer credential grants broader system access | Least Privilege scoping of the integration credential (Constitution Section 29) | Billing and Claims Module |

### Notification Channels

| STRIDE | Threat | Mitigation Category | Owner |
|---|---|---|---|
| Spoofing | Spoofed notification sender confuses/phishes a patient | Authenticated sender identity / consistent branding category | Notification Service |
| Tampering | Content altered in transit via a third-party channel | Channel-dependent; use the channel's own security where available, never relied on exclusively | Notification Service |
| Repudiation | No proof a notification was sent/received | Delivery-status audit log (Constitution Section 23) | Notification Service |
| Information Disclosure | Sensitive result content leaks via an insecure channel | Data Scope/Consent-filtered payload (Constitution Section 26, already Required) | Notification Service |
| **Denial of Service** | Channel outage | Graceful degradation category (Constitution Section 34) | **Architecture Review Board** — same pre-existing gap as above for the rate-limiting *abuse* case; outage-degradation itself is already covered by Section 34 |
| Elevation of Privilege | Not applicable — outbound-only, no inbound privilege path | N/A | N/A |

## AI Use Cases (grouped by Phase 10's Pattern A / Pattern B)

### Pattern A — High-Stakes (Use Cases #1, #3, #4)

| STRIDE | Threat | Mitigation Category | Owner |
|---|---|---|---|
| Spoofing | Spoofed AI Gateway response reaches the verifier | Gateway response authenticity; the HITL gate itself is the primary control (defense in depth) | Test Processing and Result Verification Module (candidate) |
| Tampering | AI suggestion altered before reaching the human reviewer | Integrity-protected internal channel | Same |
| Repudiation | No record of what AI suggested vs. what the human actually decided | Mandatory AI Action Audit Trail (Constitution Section 23/28, already Required — Phase 10's Gateway contract shape already includes this) | Same |
| Information Disclosure | Medical content sent to the AI Gateway (or an external provider) without minimization | Constitution Section 28's policy gate (already Accepted) | Same |
| Denial of Service | AI Gateway unavailable blocks the verifier's workflow | **Structural mitigation, not just a category:** verification must be possible *without* AI assistance — AI is advisory only, never a hard dependency of the `Verified` transition | Same — this is a design principle Phase 12 should carry into the Discovery Book explicitly |
| Elevation of Privilege | Compromised AI Gateway credential used to inject a false "verified" state | **Structural mitigation:** the AI Gateway has no write path to `ResultVerified` at all (confirmed in Phase 10's Pattern A diagram) — not a permission to restrict, a path that doesn't exist | Same |

### Pattern B — Low-Stakes (Use Cases #2, #5, #6, #7)

Same 6 categories, generally lower severity. The one category worth
stating explicitly: **Information Disclosure** — Data Scope filtering must
be enforced *after* the AI Gateway returns raw results, never delegated to
or trusted from the AI Gateway itself (confirmed in Phase 10's Pattern B
diagram). Denial of Service here only degrades convenience (search,
anomaly flags), not core operations — Low severity, no special mitigation
beyond standard graceful degradation.

### Use Case #8 (Not Ready)

Not STRIDE-analyzed for deployment — it is not accepted for use yet (Phase
10, Risk #13). No mitigation mapping is meaningful for a use case that
isn't approved to exist.

## Summary Table

| Category | Threats Identified | Mitigated (category exists) | Accepted Risk (owner named, no platform policy yet) | Unmitigated/Unowned |
|---|---|---|---|---|
| Spoofing | 5 | 5 | 0 | 0 |
| Tampering | 5 | 5 | 0 | 0 |
| Repudiation | 5 | 5 | 0 | 0 |
| Information Disclosure | 5 | 5 | 0 | 0 |
| Denial of Service | 5 | 3 | 2 (Device, Notification — pre-existing gap) | 0 |
| Elevation of Privilege | 4 (1 N/A) | 4 | 0 | 0 |

**Zero-Unmitigated-Threat Gate: satisfied.** The 2 "Accepted Risk" entries
carry a named owner (Architecture Review Board) and reference the
pre-existing, already-logged gap in `docs/constitution/REVIEW-REPORT.md`
(Open Risk R1) — consistent with Constitution Section 37's explicit
allowance for owned, accepted risk rather than requiring every gap to
block progress.
