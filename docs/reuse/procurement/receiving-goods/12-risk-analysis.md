| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| A future implementer defaults to ERPNext's built-in stock module out of convenience, silently recreating the avoided duplicate | Medium | Medium | This Feature's explicit integration contract (ERPNext matching → OpenBoxes stock API) should be enforced at SAD/implementation time, not left as a suggestion |
