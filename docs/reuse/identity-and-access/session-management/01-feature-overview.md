# Feature: Session Management

**Module:** Identity and Access (Platform Kernel). Covers token
lifecycle (access/refresh token issuance and rotation), session timeout,
concurrent-session limits, and forced logout (e.g., a Tenant Admin
revoking a compromised user's sessions — Constitution Section 21's
Break-Glass-adjacent revocation need). Same candidate pool/Engine
decision as `../authentication/`.
