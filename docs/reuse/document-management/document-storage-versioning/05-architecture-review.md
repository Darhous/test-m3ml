# Architecture Review — Document Storage / Versioning

Alfresco's repository model (versioned content nodes + metadata +
Activiti workflow) directly fits both this Feature (general storage) and
`document-control-workflow` (SOP approval) with one Engine — avoiding
the duplicate this program detected at Module 3. Deployed as a Shared
Technical Service per Wave 10, called by any Module needing document
storage (not just Audit and Compliance).
