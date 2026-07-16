# Risk Analysis — User and Group Management

Inherits `../authentication/12-risk-analysis.md`. Feature-specific:
incorrect Group-to-Branch mapping at provisioning time could grant a
staff member access beyond their intended Branch — mitigated by
provisioning being itself a Backend-enforced, audited operation
(Constitution Section 21+23), not a reason to avoid the mapping. Owner:
Tenant and Organization Management Module (provisioning trigger) +
Identity and Access Module (enforcement).
