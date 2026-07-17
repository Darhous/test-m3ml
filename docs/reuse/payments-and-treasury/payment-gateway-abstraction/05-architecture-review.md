Same pattern as Module 4's `device-protocol-adapters`: per-gateway
adapters over a common internal interface, since no single product
covers every gateway a healthcare platform in Egypt would need (Fawry,
Paymob, and potentially international processors for cross-border
billing). Omnipay's adapter-interface design (a `AbstractGateway` base
class with per-provider implementations) is a directly useful
architecture Reference regardless of the platform's eventual language
stack.
