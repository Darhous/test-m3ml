# Lifecycle

## Distinguishing This Document From What Already Exists

Three lifecycle concepts already exist in this document set, each at a
different granularity — this document adds a **fourth, platform/
product-level** granularity and does not duplicate the other three:

| Existing Document | Granularity |
|---|---|
| `04-API-GOVERNANCE.md` | Per-contract governance lifecycle (Draft → Published → Deprecated → Retired) |
| `07-VERSIONING.md` | Per-version compatibility/deprecation mechanics |
| `17-OPENAPI-GOVERNANCE.md` §Version Governance | Per-contract-document version tracking |
| **This document** | **Platform-wide release-channel and product-lifecycle framing that the above three operate within** |

## Backward Compatibility

Restates no new policy — `07-VERSIONING.md`'s Compatibility Policy and
`16-CONTRACT-FIRST.md`'s contract-testing enforcement remain the sole
mechanism. This document's contribution is organizational: backward
compatibility is a **release-channel property**, defined below, not a
per-contract afterthought.

## Release Channels

**Recommendation.** Every Published contract's version sits in exactly
one release channel at a time:

| Channel | Meaning | Consumer Expectation |
|---|---|---|
| **Alpha** | Pre-`04-API-GOVERNANCE.md`-Published; internal Module teams only, no compatibility guarantee | Breaking changes possible without notice |
| **Beta** | Published, but explicitly flagged early — typically a new Partner API candidate from `21-INTEGRATIONS.md` under active Certification | Compatibility guaranteed within Beta, but the whole Beta contract may still be revised before General Availability |
| **General Availability (GA)** | Fully Published, full `04`/`07` governance and Breaking Change Policy in force | Full compatibility and deprecation-window guarantees apply |
| **Long-Term Support (LTS)**, where designated | A GA version explicitly held stable longer than the default deprecation window, for Partner integrations with extended migration needs | Extended support window — exact duration not fixed here, same reasoning as `07-VERSIONING.md`'s unfixed deprecation duration |

Not every contract needs an LTS designation — it is reserved for
versions with active Partner dependents whose own release cadence this
platform does not control (`07-VERSIONING.md`'s Migration Rules already
name this asymmetry).

## Deprecation

Reuses `04-API-GOVERNANCE.md`'s lifecycle stage and `07-VERSIONING.md`'s
Deprecation Policy exactly. This document's addition: a Deprecation
announcement is propagated automatically to `23-API-CATALOG.md` (surfaced
to every consumer browsing that entry) and, for any Partner with an
active subscription to the affected API Product
(`25-MONETIZATION.md`), triggers a Portal notification
(`22-DEVELOPER-PORTAL.md`'s Self-Service surface) — deprecation is
communicated through the same systems a consumer already uses, not a
separate mailing-list-only process this architecture doesn't otherwise
touch.

## Migration

Reuses `07-VERSIONING.md`'s Migration Rules (written migration notes,
dual-version support during the deprecation window). This document
adds: a migration note is itself a Catalog-linked artifact
(`23-API-CATALOG.md`), discoverable from the old version's entry, not a
document a consumer has to separately locate.

## Retirement

Reuses `04-API-GOVERNANCE.md`'s Retired stage (`410 Gone`). A Retired
version's Catalog entry is archived, not deleted
(`17-OPENAPI-GOVERNANCE.md`'s Version Governance already establishes
this), preserving the platform's own historical record even after
consumer-facing access ends.

## Platform Evolution Framing

This document does not introduce a fifth compatibility mechanism — it
organizes the three already-specified mechanisms into channels a
Module team and a Partner developer can both reason about at a glance,
which is the concrete deliverable `30-ROADMAP.md`'s "Platform
Evolution" section builds on next.
