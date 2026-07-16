| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| A true critical result fails to escalate (notification delivery failure, threshold misconfiguration) | Low | Very High (direct patient-safety risk) | Multi-channel redundancy (Novu's native strength) + auto-escalation timer to a secondary recipient + immutable audit of every escalation attempt (immudb) |
| Alert fatigue from over-broad critical-value thresholds | Medium | Medium | Clinically-reviewed, analyte-specific thresholds, an implementation-time clinical-governance task, not a software one |
