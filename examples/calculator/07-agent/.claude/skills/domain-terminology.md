# Domain & Terminology

> Canonical policy version: blueprint-v2-tasks-26-e1ec194e
> Generated: 2026-10-09 10:18:38Z
> Project: E01-calculator
Architecture style: Modular Monolith.

Components:

| Component | Kind | Responsibilities |
| --- | --- | --- |
| Local Data Store | DataStore | • Provide durable, ACID-compliant persistence for all domain entities and audit events. • Enforce relational integrity, foreign key constraints, and unique indexes. • Support point-in-time recovery and snapshot durability. |
| Console Host | DeployableUnit | • Expose secure RESTful API endpoints for client and external consumers. • Enforce authentication, role-based authorization, and rate limiting. • Coordinate transactional unit-of-work across domain modules. • Emit structured audit logs and operational telemetry. |
| Calculation History | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.; The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.; The calculator shall provide a mechanism for users to view their calculation history from the SQLite database.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Error Reporting | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.; The calculator shall accurately evaluate division operations, including handling division by zero gracefully.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Expression Evaluation | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.; The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Rounding and Precision | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.; The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.; The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |

