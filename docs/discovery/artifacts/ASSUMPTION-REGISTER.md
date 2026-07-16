# Assumption Register

**Purpose:** every fact used in Discovery that is not directly Confirmed by
the user or an existing Accepted document is logged here as
`Inferred — Industry Reference`, with its source and the phase that
introduced it. Nothing in this register is `Accepted` project fact — it is
working material for Discovery, explicitly separated from Confirmed content
per the user's chosen execution mode (Assumption-Driven Autonomous Run,
approved at Discovery Program start). Every entry must be reviewed and
either Confirmed, corrected, or rejected by the user before any Software
Architecture Document work begins (Constitution Section 2/46 already
requires this kind of settling before final documents).

**Status vocabulary for this register (distinct from the Context Store's
Decision Status vocabulary, same separation principle as Constitution
Section 59):**
- `Inferred — Industry Reference`: standard, well-established laboratory/
  healthcare industry practice, not specific to this company; used to make
  Discovery executable without live stakeholder interviews per the user's
  chosen mode.
- `Inferred — Extrapolated`: derived from a Confirmed fact by reasonable
  extension (cited).
- `Pending User Confirmation`: explicitly flagged for the user to confirm/
  reject in a future review pass.

| # | Assumption | Status | Source / Basis | Phase Introduced | Confidence |
|---|---|---|---|---|---|
| 1 | The Business Capability Map's 20 capabilities (Test Ordering, Specimen Collection, Accessioning, Rejection/Recollection, Processing, Verification, Reporting, etc.) | Inferred — Industry Reference | Standard laboratory information system (LIS) operational model | 02 | Medium-High (well-established industry pattern, but not confirmed for this specific platform) |
| 2 | Core/Supporting/Generic candidate tags in the Capability Map | Inferred — Industry Reference | DDD Strategic Design lens applied to Assumption #1 | 02 | Low (explicitly Candidate; Phase 04 re-derives from real event evidence, not this tagging) |
| 3 | Four traced Value Streams (VS1–VS4) and their step outlines | Inferred — Industry Reference | Standard LIS + billing workflow pattern | 02 | Medium |
| 4 | 15 stakeholder categories' "Candidate Primary Needs" (see `.claude/context/stakeholders.md`, Discovery Phase 02 section) | Inferred — Industry Reference | Standard healthcare/lab stakeholder needs pattern | 02 | Low-Medium (needs real confirmation per category; explicitly flagged in the file itself) |
| 5 | A supplier/procurement value stream was NOT traced (gap, not an assumption) | N/A — explicit gap | Deliberately left untraced pending real input | 02 | N/A |
| 6 | Full event/command/actor chain for VS1–VS4 (26 events total) | Inferred — Industry Reference | Standard LIS event flow | 03 | Medium |
| 7 | Rejection reason taxonomy (Insufficient Volume, Hemolyzed, Clotted, Mislabeled, Wrong Container, Contaminated) | Inferred — Industry Reference | Standard specimen-QC practice | 03 | Medium-High (very standard in lab QC, but exact taxonomy for this platform unconfirmed) |
| 8 | 5 candidate Pivotal Events (`ResultVerified`, `ResultReleased`, `SpecimenAccessioned`, `SpecimenRejected`, `ClaimAdjudicated`) | Inferred — derived from Assumption #6 via handoff analysis | Event Storming method applied to Assumption #6 | 03 | Medium |
| 9 | 4 candidate missing events (equipment-failure event, failed-home-visit event, chain-of-custody handoff event, claim-denial event) were identified as gaps, not fabricated | N/A — explicit gap, logged as Hotspots H2/H4/H5/H9 | Deliberately left as gaps | 03 | N/A |

*(Populated as Discovery proceeds — see phase reports for entries added
each phase; this table is the consolidated index, kept in sync at the end
of every phase.)*
