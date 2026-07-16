# Architecture Review — Multi-Factor Authentication

Keycloak's Authentication Flows (a configurable, visual flow-builder) can
express step-up MFA (require OTP/WebAuthn only for specific Sensitive
Operations, not every login) without custom code — directly serving
Constitution Section 21's elevated-controls requirement for Sensitive
Operations (Result Verification, Payroll dual-control) without forcing
every low-risk login through the same friction. This is the
Feature-specific architectural fit finding.
