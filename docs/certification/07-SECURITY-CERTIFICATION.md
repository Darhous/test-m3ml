# Security Certification

Per this phase's explicit instruction, this document identifies
architectural risks only — it does not redesign any security control.
Grounded in the `stride-analysis-patterns` and `threat-mitigation-mapping`
Skills' methodology.

## Threat Coverage

STRIDE has now been applied at three distinct points across this
repository's history, and this audit verifies they are consistent, not
redundant-and-contradictory:

| Application | Location | Scope |
|---|---|---|
| 1 | `docs/discovery/reports/11-stride-mitigation-mapping.md` | Discovery-phase, business-process-level threats |
| 2 | `docs/api-platform/11-API-SECURITY.md` | API Gateway/Module boundary-level threats |
| 3 | `docs/api-platform/19-WEBHOOKS.md` (via `threat-mitigation-mapping` Skill) | Outbound webhook-delivery-specific threats (SSRF, signing) |

**Finding: complementary, not overlapping-and-contradictory** — each
application targets a different architectural layer (business process,
API boundary, outbound delivery channel), consistent with defense-in-
depth. No STRIDE category is left completely uncovered at every layer;
Spoofing/Tampering/Repudiation/Information-Disclosure/DoS/Elevation are
each addressed at the layer(s) where they are actually exploitable.

## Trust Boundaries

Verified consistent across `docs/constitution/PROJECT-CONSTITUTION.md`
§20-21 (Authentication/Authorization Rules), ADR-0008, and
`docs/api-platform/02-API-FIRST-ARCHITECTURE.md`'s five-layer model:
the trust boundary is drawn at the Edge Gateway (external) and
re-drawn at every Module boundary (internal, defense-in-depth) —
**never at the UI layer alone**, directly satisfying CLAUDE.md §14's
explicit requirement and Constitution's Accepted Constraint #12 ("UI
hiding is never an Authorization control").

## Identity / Authentication / Authorization

- **Identity**: single source of truth (Keycloak, E1) — verified no
  second, parallel identity mechanism exists anywhere in the repository
  (grep for alternative auth schemes across `docs/` found none).
- **Authorization**: two independently-enforced PEPs (Gateway RBAC +
  Module ABAC/Data-Scope), consistent with `09-AUTHORIZATION.md` and
  re-verified against Constitution §21.
- **Risk identified (architectural, not a redesign)**: the exact
  Keycloak realm-partitioning mechanism (realm-per-Tenant vs.
  shared-realm-with-tenant-claim) remains tied to Open Question #15 —
  this is a **known, already-tracked dependency**, not a newly
  discovered gap.

## Secrets / Key Management / Vault Strategy

Already comprehensively self-disclosed as an open gap in
`docs/api-platform/12-SECRETS-AND-KEYS.md` and Open Question #29 —
this audit's independent check confirms no Secrets Engine exists
anywhere in the Technology Baseline, and no document anywhere silently
assumes one. **Architectural risk**: until a Vault-style Engine is
selected, the *behavioral requirements* `12` specifies (centralized
storage, audited access, dynamic credentials) are unenforceable by any
concrete mechanism — correctly flagged in that document as a
SAD-blocking dependency, not newly discovered here.

## API Security

See `06-API-CERTIFICATION.md`'s OWASP Top 10 re-verification (10/10
categories mapped, re-checked). No architectural gap found beyond what
`docs/api-platform/11-API-SECURITY.md` itself already discloses
(replay protection for webhook-style async callbacks explicitly
deferred to Part 2's own Webhooks document, which this audit confirms
does address it in `19-WEBHOOKS.md`, closing that specific forward
reference correctly).

## Tenant Isolation

Verified structurally sound: token-claim + header cross-check
(`14-MULTI-TENANCY.md`), Data-Scope PEP at every Module boundary,
`404`-not-`403` on out-of-scope resources (anti-enumeration). **No
architectural gap found** — the one dependency (partitioning technology,
Open Question #15) is already tracked and does not block the isolation
*model* from being sound regardless of which partitioning technology is
eventually chosen (explicitly verified as a design goal in `14`, and
re-confirmed true by this audit's re-reading of the isolation logic,
which genuinely does not depend on the partitioning mechanism).

## Data Protection / Encryption

TLS 1.2+ in transit (Recommendation, `11-API-SECURITY.md`); at-rest
encryption deferred to ADR-0005's dedicated-database tier mechanics
(not re-specified, correctly avoiding duplication). No architectural
gap found beyond what is already disclosed as unfixed-pending-real-data
(e.g., exact rotation cadences).

## Logging / Audit Trail

immudb (E4)-backed, tamper-evident, dedicated to Sensitive Operations
and Break-Glass — verified structurally separate from general
operational logging (`docs/api-platform/27-OBSERVABILITY.md`
explicitly declines to merge the two streams, correctly preserving the
audit trail's independence). Full Auditability (Accepted Architecture
Principle #10) is consistently invoked wherever a Sensitive Operation
is discussed — no document treats an operational log as a substitute
for the audit trail.

## Compliance Readiness

Constitution §31 (Compliance Readiness Rules) exists but is explicitly
not a legal compliance certification (stated in `docs/constitution/
README.md`'s own "What this is not" section) — this audit does not
treat it as one either. Egypt-market-specific regulatory gaps (Cross-
Border Transfer under Law 151/2020, Labor Law/Social Insurance impact
on Payroll, National ID field requirement) remain correctly flagged as
`Requires Legal Verification` in `.claude/context/open-questions.md`
#25-27, not silently assumed resolved.

## Architectural Risks Identified (Consolidated — no redesign proposed)

| Risk | Layer | Severity | Already Tracked? |
|---|---|---|---|
| Vault/Secrets Engine not selected | Secrets Management | Medium | Yes — Open Question #29 |
| API Gateway not selected | Edge/Trust Boundary | Medium | Yes — Open Question #28 |
| Tenant-partitioning technology undecided | Data Isolation | Medium | Yes — Open Question #15 |
| AGPL legal review outstanding (5 Engines) | Licensing/Compliance | High | Yes — `08-AGPL-LEGAL-CHECKLIST.md`, R-04 |
| Egypt regulatory research incomplete (3 items) | Compliance | Medium | Yes — Open Questions #25-27 |
| Mirth Connect frozen-release (no free security patches) | Device Integration | High | Yes — R-02 |

**No new, previously-untracked architectural security risk was
discovered by this audit.** Every risk identified above was already
present in the repository's own Risk Register(s) — this is a positive
certification signal (the project's own risk-surfacing discipline is
already comprehensive), consolidated in full in `11-RISK-REGISTER.md`.

## Certification Verdict

**PASS WITH CONDITIONS.** No architectural security design flaw found.
Security posture is sound and consistently layered. Certification is
conditional on the same 6 already-tracked items above being resolved
before their respective finalization points — none blocks SAD *work
starting*, consistent with `docs/architecture-review/
13-READINESS-FOR-API-STRATEGY.md`'s own established distinction between
blocking-to-start vs. blocking-to-finalize.
