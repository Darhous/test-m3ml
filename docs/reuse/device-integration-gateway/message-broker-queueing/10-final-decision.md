# Final Decision — Message Broker / Queueing

## Decision: **ENGINE + ADAPTER**

**Engine:** RabbitMQ (MPL 2.0). Retroactively confirms the "durable,
at-least-once broker delivery" requirement flagged but left unspecified
in Module 1 (`audit-hooks-integration`) and Module 3
(`immutable-audit-trail`) — those Features' integration notes now resolve
to this concrete choice.
