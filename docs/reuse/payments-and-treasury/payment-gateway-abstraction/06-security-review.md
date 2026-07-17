Payment-card data is a PCI-DSS-relevant surface — implementation-time
requirement to use gateway-hosted tokenization/checkout (Fawry/Paymob
both offer hosted checkout options per this pass's search) rather than
handling raw card data in the platform's own systems, minimizing PCI
scope. Not a program-level product finding, but an architecturally
significant constraint to carry forward to the SAD.
