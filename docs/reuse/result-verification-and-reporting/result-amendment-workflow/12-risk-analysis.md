| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| An amendment is made without notifying all prior recipients of the original result | Low-Medium | High (clinical decisions may have already been made on stale data) | Mandatory re-notification step in the amendment workflow, tied to the original distribution list |
| Amendment overwrites rather than versions the original, losing audit history | Low | High | Immutable prior-version write to immudb enforced at the Aggregate level, not optional |
