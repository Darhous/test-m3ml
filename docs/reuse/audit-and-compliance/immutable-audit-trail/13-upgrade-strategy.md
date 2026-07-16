# Upgrade Strategy — Immutable Audit Trail

Track immudb's release cadence (1.11 shipped May 2026) for both features
and any OSS-to-Enterprise feature migration signals (open-core risk,
same discipline applied to Authentik/Unleash). Because the audit-write
API is a narrow, stable contract (write record, verify chain), a future
migration to Trillian or another tamper-evident store — should immudb's
licensing trajectory ever require it — is bounded to the Audit and
Compliance Module's own write-adapter, not a platform-wide change.
