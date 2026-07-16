# Integration Options — Multi-Channel Notification Engine

Deployed as the ADR-referenced Independent Component (Constitution
Section 11), invoked by other Modules via a single "send notification"
event through the platform's own RabbitMQ broker (Module 4) — no Module
calls Novu's API directly, preserving the Independent Component
boundary.
