# Build vs. Buy — Patient Registry / MPI

**REFERENCE (FHIR Patient resource) + BUILD (platform-owned Aggregate).**
Not a traditional weighted comparison — OpenMRS was evaluated and
explicitly rejected as an *adopt-the-whole-system* option because it
would displace this platform's own Core Domain (ADR-0011 Amended), the
single most consequential "don't reuse" finding in the entire program.
Reusing FHIR's proven data-model shape (not its implementation) is the
correct middle ground: real reuse without surrendering the Core Domain.
