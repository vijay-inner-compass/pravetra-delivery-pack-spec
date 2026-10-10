# Architecture Summary

| Field | Value |
| --- | --- |
| Architecture style | Modular Monolith |
| Decomposition | ModularMonolith |
| Branching strategy | Trunk-based development |

Rationale: A single deployable unit keeps operational overhead low while the project's current scope stays small.

## Selected Technology

- **Technology**: C# on .NET 10 as a console application, tested with xUnit (rejected alternatives, do not use: Python 3 script tested with pytest (the team knows .NET; a Python runtime would have to be installed on analyst laptops); F# on .NET 10 (no team experience)). Rationale: Implementation language and test framework. The team already knows C# and .NET, and System.Decimal avoids the binary floating-point errors that are the core problem. The owner mandates .NET for the showcase.
- **Technology**: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (rejected alternatives, do not use: a JSON file rewritten after every calculation (no transactions; a crash mid-write corrupts the history); a plain-text file with one line per calculation (same weakness, and no way to enforce the last-10 rule atomically)). Rationale: Storage for the calculation history. SQLite is the mandated database. It gives transactional writes, survives a crash mid-write, needs no server and is one file to back up or delete.
- **Technology**: System.Decimal for arithmetic operations (rejected alternatives, do not use: double for arithmetic operations). Rationale: System.Decimal is the preferred choice for this project due to its ability to handle financial calculations accurately. The requirement for precise arithmetic evaluation (R10) and the need to avoid floating-point inaccuracies make System.Decimal the only viable option. Switching to double would compromise the integrity of the calculations, which is unacceptable given the project's goals.
- **Technology**: Console.ReadLine for user input (rejected alternatives, do not use: Command-line arguments for user input). Rationale: Both input methods are viable, but Console.ReadLine is preferred for its simplicity and direct interaction with users. Command-line arguments can be considered for advanced use cases where batch processing is needed.
- **Technology**: Decimal rounding for results (rejected alternatives, do not use: String formatting for output). Rationale: Decimal rounding is essential for financial accuracy, while string formatting enhances user experience. Both should be implemented to ensure the calculator meets its functional requirements.
- **Technology**: Console.Error for error messages (rejected alternatives, do not use: Throwing exceptions for error handling). Rationale: Both options provide mechanisms for handling errors gracefully, but using Console.Error aligns with the requirement for clear user feedback without crashing the application.

## Component Catalog

| Component | Kind | Responsibilities |
| --- | --- | --- |
| Local Data Store | DataStore | • Provide durable, ACID-compliant persistence for all domain entities and audit events. • Enforce relational integrity, foreign key constraints, and unique indexes. • Support point-in-time recovery and snapshot durability. |
| Console Host | DeployableUnit | • Expose secure RESTful API endpoints for client and external consumers. • Enforce authentication, role-based authorization, and rate limiting. • Coordinate transactional unit-of-work across domain modules. • Emit structured audit logs and operational telemetry. |
| Calculation History | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.; The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.; The calculator shall provide a mechanism for users to view their calculation history from the SQLite database.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Error Reporting | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.; The calculator shall accurately evaluate division operations, including handling division by zero gracefully.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Expression Evaluation | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.; The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Rounding and Precision | LogicalModule | • Implement core domain logic and invariant validation for: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.; The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.; The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |

