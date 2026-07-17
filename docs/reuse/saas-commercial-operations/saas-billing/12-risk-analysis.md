| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Confusion between this Feature (platform SaaS revenue) and Module 21's `invoicing-engine` (lab service revenue) among future implementers | Low-Medium | Medium | Explicit disambiguation in this file and `MASTER_DEPENDENCY_MATRIX.md`, consistent with the program's other proactive-avoidance findings |
| A custom Kill Bill payment plugin for Fawry/Paymob (Module 22) is nontrivial engineering effort | Medium | Low-Medium | Budget explicitly at SAD time; Kill Bill's existing Stripe/Adyen/GoCardless plugins may suffice for international card payments even if local-gateway support needs custom work |
