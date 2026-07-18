# Observability

## Foundation Already Laid in Part 1

**Fact.** `05-API-STANDARDS.md` already mandated Correlation ID
propagation platform-wide, explicitly noting "full distributed tracing
is explicitly Part 2... this Recommendation establishes only the
identifier discipline that Observability will later build on." This
document is that build-out — it does not re-specify the identifier
scheme, it specifies what is built on top of it.

## Metrics

**Recommendation.** Every layer in `02-API-FIRST-ARCHITECTURE.md`
emits standard request metrics (rate, error rate, duration) tagged
with: Module, endpoint, API type (`03-API-DOMAIN-INVENTORY.md`),
Tenant ID, and lifecycle stage (`04-API-GOVERNANCE.md`) of the version
being called. Tagging by lifecycle stage specifically lets the
platform observe whether a Deprecated version still has live traffic
before Retirement — the concrete operational signal
`07-VERSIONING.md`'s "no version may be Retired while it has any known
active Partner consumer" qualitative floor needs to actually be
checked against.

## Logging

**Recommendation.** Structured (not free-text) logs, correlated by
Correlation ID, at the Gateway and every Module boundary
(`02`). A Sensitive Operation (`ResultVerified`, `ResultReleased`,
Break-Glass) produces both an operational log entry *and* the separate,
immutable Audit Event already required by
`09-AUTHORIZATION.md`/`11-API-SECURITY.md` — these are two different
things serving two different purposes (operational debugging vs.
tamper-evident compliance record via immudb, E4) and this document does
not merge them into one stream, which would weaken the audit
guarantee's independence.

## Tracing

**Recommendation.** Distributed traces span the full request lifecycle
(`02-API-FIRST-ARCHITECTURE.md`: Gateway → Routing → Module → Aggregate
→ Anti-Corruption Layer), using the Correlation ID as (or alongside) the
trace identifier, so an operator can follow one request across every
layer it touches — including, where relevant, the async hop into
`18-ASYNCAPI-EVENTS.md`'s event bus, which already carries
`correlationId` on every event specifically to make this cross-protocol
tracing possible.

## Dashboards

**Fact-grounded Recommendation.** Apache Superset (Technology Baseline
E10, Apache-2.0) is already the ratified BI/Analytics engine, owned by
the Analytics Module (`03-API-DOMAIN-INVENTORY.md`). API operational
dashboards (traffic, error rate, latency, quota consumption) are built
on the same metrics/log pipeline above and are a natural consumer of
Superset — **this Board recommends reusing Superset for API dashboards
rather than introducing a second BI tool**, since the evaluation
criteria that matter (self-hosted, Apache-2.0, already integrated with
this platform) are unchanged by the fact that the data source is API
telemetry rather than business data. Whether Superset alone is
sufficient for API-specific analytics with the depth an API Analytics
product (Moesif-style consumer-level breakdowns, anomaly detection) would
offer is a distinct, open question — see `31-ENTERPRISE-PRODUCT-
DECISIONS.md`.

## API Analytics vs. Usage Analytics

Two distinct audiences, both fed by the same metering pipeline
(`26-BILLING.md`'s Usage Metering):

- **API Analytics** (platform-operator-facing): traffic patterns,
  error hotspots, version-adoption curves, feeds `30-ROADMAP.md`
  prioritization.
- **Usage Analytics** (Tenant/Partner-facing): the consumption view
  already specified in `22-DEVELOPER-PORTAL.md`'s Self-Service section
  and `26-BILLING.md`'s Consumption section — this document does not
  duplicate that specification, only notes it draws from the same
  underlying metrics.

## Audit

**Fact**, reused not reinvented: Audit and Compliance's immudb-backed
trail (E4) remains the single system of record for every Sensitive
Operation and every Break-Glass invocation (`09-AUTHORIZATION.md`).
Observability's logging/tracing/metrics pipeline is a *complement* to
that audit trail, never a *substitute* for it — an operational log
retention policy shorter than the audit trail's own is acceptable;
the reverse (auditing relying on operational logs that can be pruned)
would silently weaken Full Auditability (Accepted Architecture
Principle #10) and is explicitly not this document's design.

## Explicit Boundary

SLA measurement (`28-SLA.md`'s SLIs) is *derived from* this
Observability pipeline's metrics but is specified separately, since an
SLI is a commercial/contractual commitment built on top of an
operational metric, not the metric itself.
