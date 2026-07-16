# Upgrade Strategy — Message Broker / Queueing

Track RabbitMQ's release cadence under Broadcom stewardship (post-VMware
acquisition) for any commercial-tier feature migration signals, the same
open-core-drift discipline applied to Unleash/Authentik. AMQP 0-9-1
protocol stability means a future broker swap, if ever needed, is bounded
to producer/consumer connection configuration, not message-format
rewrites.
