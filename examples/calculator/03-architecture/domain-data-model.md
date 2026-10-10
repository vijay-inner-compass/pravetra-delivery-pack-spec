# Domain Data Model & Entity Dictionary

This document specifies the **Domain Data Model, Entity Boundaries, and Schema Requirements** for **E01-calculator**. It provides the persistence models, aggregate roots, relationships, and data governance rules required for autonomous coding agents implementing **TASK-001 (Primary Database / Persistence)** and component domain services across **Domain-Driven Design (DDD)**, **Scrum Data Modeling**, **SAFe Architecture Enablers**, and **Enterprise Database Engineering**.

## 1. Architecture & Persistence Context

| Architecture Attribute | Specification |
| --- | --- |
| Architecture Style | Modular Monolith |
| Decomposition Structure | ModularMonolith |
| Target Schema Version | v2 |

### Decided Persistence Stack

- **Technology**: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (rejected alternatives, do not use: a JSON file rewritten after every calculation (no transactions; a crash mid-write corrupts the history); a plain-text file with one line per calculation (same weakness, and no way to enforce the last-10 rule atomically)). Rationale: Storage for the calculation history. SQLite is the mandated database. It gives transactional writes, survives a crash mid-write, needs no server and is one file to back up or delete.
- **Technology**: Decimal rounding for results (rejected alternatives, do not use: String formatting for output). Rationale: Decimal rounding is essential for financial accuracy, while string formatting enhances user experience. Both should be implemented to ensure the calculator meets its functional requirements.

## 2. Component Entity & Schema Specifications

| Component | Kind | Responsibilities | Data Design & Entities |
| --- | --- | --- | --- |
| Local Data Store | DataStore | • Provide durable, ACID-compliant persistence for all domain entities and audit events. • Enforce relational integrity, foreign key constraints, and unique indexes. • Support point-in-time recovery and snapshot durability. | Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). |
| Console Host | DeployableUnit | • Expose secure RESTful API endpoints for client and external consumers. • Enforce authentication, role-based authorization, and rate limiting. • Coordinate transactional unit-of-work across domain modules. • Emit structured audit logs and operational telemetry. | Coordinates database transactions across modules; manages connection lifetimes and migration application. |
| Calculation History | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.; The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.; The calculator shall provide a mechanism for users to view their calculation history from the SQLite database.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |
| Error Reporting | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.; The calculator shall accurately evaluate division operations, including handling division by zero gracefully.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |
| Expression Evaluation | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.; The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |
| Rounding and Precision | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.; The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.; The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |

## 3. Entity Details & Data Governance Notes

### Local Data Store (DataStore)

- **Domain Responsibilities**: • Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Data Design & Schema Notes**: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own).
- **API & Query Interface**: Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.
- **Boundary Rationale**: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

### Console Host (DeployableUnit)

- **Domain Responsibilities**: • Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Data Design & Schema Notes**: Coordinates database transactions across modules; manages connection lifetimes and migration application.
- **API & Query Interface**: HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.
- **Boundary Rationale**: Core deployable boundary hosting API surface and domain logic as a cohesive ModularMonolith unit, balancing maintainability and deployment simplicity.

### Calculation History (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.; The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.; The calculator shall provide a mechanism for users to view their calculation history from the SQLite database..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

### Error Reporting (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.; The calculator shall accurately evaluate division operations, including handling division by zero gracefully..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

### Expression Evaluation (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.; The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

### Rounding and Precision (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.; The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.; The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

## 4. Coding Agent Implementation Rules for TASK-001 (Database & Persistence)

When implementing database schema, migrations, and entities:
1. **Strict Boundary Conformance**: Implement only the tables, aggregates, and fields required by the domain specifications above and referenced requirements. Do not invent unapproved tables or bypass entity ownership boundaries.
2. **Auditability & Temporal Tracking**: Every primary persistence entity must include audit tracking fields (`CreatedAt`, `UpdatedAt`) and strong unique identifier keys (e.g. UUID/GUID or identity keys).
3. **Referential Integrity & Cascades**: Foreign keys must have explicit delete behaviors (avoid inadvertent cascading deletions on primary aggregates; use soft deletes or fail-closed foreign key checks where appropriate).
4. **Zero-Migration Loss**: Migrations must be additive, forward-compatible, and idempotent. Never mutate applied migrations in place.
5. **Data Protection & Classification**: Ensure restricted data, credentials, and PII are marked for encryption at rest and never logged in plain text.
