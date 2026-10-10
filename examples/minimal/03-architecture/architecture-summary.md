# Architecture Summary

- **Topology**: HTTP JSON API
- **Persistence**: EF Core with PostgreSQL
- **Key Decisions**:
  - `ADR-001`: Use record types for immutable DTOs.
  - `ADR-002`: Use MediatR for in-process request dispatch.
