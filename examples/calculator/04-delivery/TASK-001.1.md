# TASK-001.1 — Maintain a local SQLite database to store the last 10

- **Component:** Local Data Store · sub-task of TASK-001 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Maintain a local SQLite database to store the last 10 calculations, allowing users to access calculation history.
> **Requirement:** The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.

## Done when
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.
- Also: Acceptance (negative) for [Must] The calculator shall maintain a local SQLite database to ...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Must] The calculator shall maintain a local SQLite database to ...: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.

## Out of scope
- the other sub-tasks of this component - TASK-001.2 (Ensure data retention by maintaining the last 10).
- the responsibilities of the other components - Calculation History, Error Reporting, Expression Evaluation, Rounding and Precision, Console Host.

## Applicable decisions
- [6b86061daec44e2d9a7ac0d88388e6c6] Technology: C# on .NET 10 as a console application, tested with xUnit
- [245f0843a31d48bcb3bfea5a95f1099a] Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite
- [d24a599f6c4f4760a7e7251ca0673579] Technology: System.Decimal for arithmetic operations
- [efb7f32edda64c679b9b293d2f4af6b3] Technology: Console.ReadLine for user input
- [ca47ae8c4ad8485ab6351de4376c04c3] Technology: Decimal rounding for results
- [021ab9627bfe41aa9d543550dffc57d1] Technology: Console.Error for error messages
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (2 listed), each shown by a named test or check.
- [ ] Every test under "Write these tests first" exists, failed before the change, and passes now.
- [ ] The applicable decisions and the common rules are respected and nothing contradicts them.
- [ ] The out-of-scope items are untouched.
- [ ] No unrelated changes: the diff stays inside the allowed paths and only this sub-task's behaviour changed.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 as a console application, tested with xUnit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file accessed with Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (System.Decimal for arithmetic operations).
- Do not substitute, replace, or alter the locked decision for Technology (Console.ReadLine for user input).
- Do not substitute, replace, or alter the locked decision for Technology (Decimal rounding for results).
- Do not substitute, replace, or alter the locked decision for Technology (Console.Error for error messages).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) localdatastore/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (localdatastore/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Local Data Store'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-001 builds and its health check passes.
2. Implement: The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own).
6. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.

## Quality and Security (this task)
- Data handling and retention specification: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own).
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.
- Non-functional target (The calculator shall evaluate arithmetic expressions quic...): The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.
- Non-functional target (The calculator shall be available to analysts whenever th...): The calculator shall be available to analysts whenever they work, because it runs locally on their laptop and needs no network or external service.
- Non-functional target (The calculator shall use decimal arithmetic for all calcu...): The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.
- Non-functional target (The calculator shall provide audit logging of all calcula...): The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.
- Non-functional target (The calculator shall ensure data retention by maintaining...): The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database.
- Non-functional target (The calculator shall be maintainable with a low operation...): The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
- Non-functional target (The calculator shall ensure compliance with internal data...): The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.
- Non-functional target (The calculator shall ensure that all arithmetic operation...): The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.

## Current State Evidence
Builds on the skeleton of 'Local Data Store' delivered by TASK-001. Greenfield component per Solution Blueprint. Target responsibilities:
• Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Source references:** BlueprintComponent: Local Data Store (`08b2b1be89c342198780376b886bff61`); Requirement: [Must] Maintain a local SQLite database to store the last 10 calculations (`ec3833c88034437e953a855512acf436`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
