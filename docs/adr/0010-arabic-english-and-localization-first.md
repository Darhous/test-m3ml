# 0010: Arabic/English and Localization First

## Status

Accepted

## Context

The platform's target users (per `stakeholders.md` and the general project
framing) are expected to include Arabic-speaking and English-speaking
users, with the architecture needing to allow additional markets/languages
later (exact target markets remain `Open`, `open-questions.md` #1, #12).
Healthcare platforms are also sensitive to correct locale-aware date,
number, address, currency, and timezone handling, given medical and
financial data involved (results timestamps, billing amounts, appointment
times across branches/timezones).

## Decision

The platform supports **Arabic and English from the beginning**, with
**RTL and LTR** UI support, **Multi-Currency**, **Multi-Timezone**, and
locale-aware date/number/address formatting, as v1 architectural
requirements rather than later add-ons. Domain models and contracts must
not hardcode a single language, currency, or timezone assumption, so that
additional markets/languages can be added later without a structural
rewrite.

## Alternatives Considered

- **English-only for v1, localization added later.** Rejected: explicitly
  contradicts the user-approved decision that Arabic and English support
  (and RTL/LTR) are required from the beginning, and retrofitting RTL
  support and locale-aware formatting into domain models later is
  typically a much larger rewrite than designing for it from the start.
- **Hardcode a single currency/timezone for the initial market.**
  Rejected: conflicts with the explicit Multi-Currency/Multi-Timezone
  requirement and would block multi-branch operation across timezones
  even within a single tenant.
- **Arabic + English + RTL/LTR + Multi-Currency + Multi-Timezone +
  locale-aware formatting, with the architecture open to more
  languages/markets later.** **Chosen.** Matches the explicit, user-approved
  decision set exactly.

## Positive Consequences

- Avoids a costly later rewrite of domain models/UI to retrofit RTL and
  locale-awareness.
- Multi-branch operation across timezones and multi-tenant operation across
  currencies are supported by design, not as exceptions.
- Sets a clear constraint (no hardcoded locale assumptions) that keeps
  future market expansion from requiring structural changes.

## Negative Consequences

- More upfront design discipline required (e.g., every date/amount/address
  field must carry or resolve locale/currency/timezone context) compared to
  a single-locale design.
- RTL UI support adds design/testing surface area from v1.

## Risks

- **Hardcoded locale assumption slipping into a domain model or contract**
  (e.g., an amount field with no currency, a timestamp with an implicit,
  undocumented timezone). Mitigated by a localization review checking
  domain models/contracts for hardcoded locale assumptions (Constitution
  Section 32).
- **RTL support treated as a pure UI/CSS concern and neglected at the
  content/data level** (e.g., mixed-direction text handling in stored
  data). Flagged for SAD-level UI/content design attention.

## Verification

- Localization review: domain models/contracts checked for hardcoded
  locale/currency/timezone assumptions.
- RTL/LTR rendering check at UI review time (once UI implementation
  begins — out of scope for this task, but the requirement is fixed now).

## Revisit Triggers

- Answers to `open-questions.md` #1/#12 (target markets, additional
  languages/currencies) extend the supported set but do not reverse the
  Arabic/English/RTL/LTR/Multi-Currency/Multi-Timezone baseline established
  here.
