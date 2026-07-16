# Security Review — Patient Registry / MPI

No independent Engine adopted, so no new CVE surface. Patient identity
data is the platform's most sensitive Core Domain data — inherits
Module 2's RLS tenant isolation and Module 3's consent/audit
requirements in full, with no exception for being "just identity data."
