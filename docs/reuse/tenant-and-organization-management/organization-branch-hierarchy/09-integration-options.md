# Integration Options — Organization / Branch Hierarchy

Branch ID shared as the join key between the Keycloak Group hierarchy
(Module 1) and this Feature's business-data table, kept in sync via the
`TenantProvisioned`/`BranchCreated` Domain Events (Wave 5 vocabulary) —
not two independently maintained hierarchies.
