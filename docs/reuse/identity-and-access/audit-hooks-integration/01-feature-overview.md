# Feature: Audit Hooks Integration

**Module:** Identity and Access (Platform Kernel). Covers emitting every
identity-relevant event (login, logout, failed login, role change,
session revocation) into the platform's own immutable Audit trail
(Constitution Section 23), owned by the Audit and Compliance Module
(researched separately, `../../audit-and-compliance/`). This Feature is
the **boundary** between the two Modules, not a duplicate of either.
