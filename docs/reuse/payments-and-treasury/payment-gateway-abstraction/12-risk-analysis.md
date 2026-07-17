| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Raw card data touching platform systems creates unnecessary PCI-DSS scope | Medium | High | Use gateway-hosted tokenization/checkout (Fawry/Paymob both support this), an implementation-time architectural constraint |
| Single-gateway lock-in if the abstraction layer isn't genuinely provider-neutral | Low-Medium | Medium | Omnipay's adapter-pattern Reference exists specifically to avoid this |
