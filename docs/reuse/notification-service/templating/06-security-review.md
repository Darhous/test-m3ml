# Security Review — Templating

Inherits `../multi-channel-notification-engine/06-security-review.md`.
Template-injection risk (user-supplied data rendered unsafely into a
template) is a generic web-security concern requiring standard output
encoding — an implementation-time discipline, not a product defect.
