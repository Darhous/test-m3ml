| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| A misconfigured OPA policy silently over-permits result verification | Low-Medium | Very High (Sensitive Operation, patient-safety-critical) | Policy-as-code review + staging environment policy testing, an implementation-time control; already flagged generally at Module 1 |
| AI-assisted flagging (if adopted per Module 6's Portkey Gateway) is mistaken for final verification | Low | Very High | Explicit UI/workflow separation between AI-assisted flagging and human sign-off, per Project Instruction #15 |
