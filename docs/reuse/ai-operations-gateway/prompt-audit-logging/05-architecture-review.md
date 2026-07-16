# Architecture Review — Prompt Audit Logging

Portkey captures request/response at the Gateway; the platform's own
adapter forwards each record through RabbitMQ (Module 4) into immudb
(Module 3) for long-term immutable retention — Portkey's own logs are
operational/short-term, immudb is the compliance-grade record.
