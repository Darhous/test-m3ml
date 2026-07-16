# Architecture Review — Organization / Branch Hierarchy

The Keycloak Group hierarchy (Module 1) and this Feature's business-data
table should share the same identifiers (Branch ID consistent across
both systems) to avoid two independently-drifting hierarchies — a direct
architectural dependency this research surfaces between two Features.
