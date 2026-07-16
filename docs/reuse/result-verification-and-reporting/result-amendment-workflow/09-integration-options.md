Extends `result-review-verification-workflow`'s Verification Aggregate;
calls OPA (Module 1) for the amendment-authorization gate; writes the
prior-version record to immudb (Module 3); re-triggers
`clinical-report-generation` and, if applicable,
`critical-result-escalation` (this Module) for re-notification.
