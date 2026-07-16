# Feature: HL7 Integration Engine

**Module:** Device Integration Gateway (Independent Component, ADR 0006)
**Source:** Wave 3 "Device Integration" (Evidenced, Baseline); Constitution
Section 24 (Device Integration, readiness list HL7 v2/ASTM/Vendor API).

Receives, transforms, and routes HL7 v2/v3/CDA/FHIR messages between lab
analyzers/external systems and the platform, without corrupting core data
on device failure (Section 24's explicit requirement).
