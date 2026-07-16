# Architecture Review — E-Signature

Documenso's more modern stack and published SOC 2 compliance work is a
better architectural-trust fit for a regulated healthcare platform than
OpenSign's less-mature, unbacked profile — integrated as a standalone
signing service, output (signed document + audit certificate) stored in
Alfresco (`document-storage-versioning`).
