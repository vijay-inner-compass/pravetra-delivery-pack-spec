# JetBrains Junie Agent Guidelines

> Canonical policy version: blueprint-v2-tasks-26-e1ec194e
> Generated: 2026-10-09 10:18:38Z
> Project: E01-calculator
## Mission

Deliver the 26 tasks in the specified dependency order to implement the Solution Blueprint for project 'E01-calculator', adhering strictly to the recorded architecture style of Modular Monolith and without inventing any additional architecture, data models, or public contracts.

## Architecture

Modular Monolith

## Tasks

- TASK-001 - Scaffold Local Data Store (DataStore) - not_started - depends on: (none)
  - TASK-001.1 - Maintain a local SQLite database to store the last 10 - not_started - depends on: TASK-001
  - TASK-001.2 - Ensure data retention by maintaining the last 10 - not_started - depends on: TASK-001
- TASK-002 - Scaffold Calculation History (LogicalModule) - not_started - depends on: TASK-001
  - TASK-002.1 - Provide audit logging (+1 related Should requirement) - not_started - depends on: TASK-002
  - TASK-002.2 - Delete calculation history from the SQLite database - not_started - depends on: TASK-002
- TASK-003 - Scaffold Error Reporting (LogicalModule) - not_started - depends on: TASK-001
  - TASK-003.1 - Provide clear error messages for malformed expressions - not_started - depends on: TASK-003
  - TASK-003.2 - Accurately evaluate division operations - not_started - depends on: TASK-003
- TASK-004 - Scaffold Expression Evaluation (LogicalModule) - not_started - depends on: TASK-001
  - TASK-004.1 - Evaluate arithmetic expressions - not_started - depends on: TASK-004
  - TASK-004.2 - Evaluate arithmetic expressions quickly enough - not_started - depends on: TASK-004
- TASK-005 - Scaffold Rounding and Precision (LogicalModule) - not_started - depends on: TASK-001
  - TASK-005.1 - Handle rounding using decimal arithmetic to avoid - not_started - depends on: TASK-005
  - TASK-005.2 - Use decimal arithmetic for all calculations to ensure - not_started - depends on: TASK-005
  - TASK-005.3 - All arithmetic operations are performed - not_started - depends on: TASK-005
- TASK-006 - Scaffold Console Host (DeployableUnit) - not_started - depends on: TASK-001, TASK-002, TASK-003, TASK-004, TASK-005
  - TASK-006.1 - Reduce the error rate in invoice total calculations - not_started - depends on: TASK-006
  - TASK-006.2 - Minimize rework time associated - not_started - depends on: TASK-006
  - TASK-006.3 - Run locally on each analyst's laptop - not_started - depends on: TASK-006
  - TASK-006.4 - Available to analysts whenever they work - not_started - depends on: TASK-006
  - TASK-006.5 - Input arithmetic expressions directly into the terminal - not_started - depends on: TASK-006
  - TASK-006.6 - Ensure the command-line calculator is compatible - not_started - depends on: TASK-006
  - TASK-006.7 - Ensure compliance with internal data handling policies - not_started - depends on: TASK-006
  - TASK-006.8 - Ensure the command-line calculator provides accurate results - not_started - depends on: TASK-006
  - TASK-006.9 - Provide built-in help documentation (+2 related Should requirements) - not_started - depends on: TASK-006

## Task Dependencies

| Task | Depends On | Unlocks |
| --- | --- | --- |
| TASK-001 | (none) | TASK-001.1, TASK-001.2, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006 |
| TASK-001.1 | TASK-001 | (none) |
| TASK-001.2 | TASK-001 | (none) |
| TASK-002 | TASK-001 | TASK-002.1, TASK-002.2, TASK-006 |
| TASK-002.1 | TASK-002 | (none) |
| TASK-002.2 | TASK-002 | (none) |
| TASK-003 | TASK-001 | TASK-003.1, TASK-003.2, TASK-006 |
| TASK-003.1 | TASK-003 | (none) |
| TASK-003.2 | TASK-003 | (none) |
| TASK-004 | TASK-001 | TASK-004.1, TASK-004.2, TASK-006 |
| TASK-004.1 | TASK-004 | (none) |
| TASK-004.2 | TASK-004 | (none) |
| TASK-005 | TASK-001 | TASK-005.1, TASK-005.2, TASK-005.3, TASK-006 |
| TASK-005.1 | TASK-005 | (none) |
| TASK-005.2 | TASK-005 | (none) |
| TASK-005.3 | TASK-005 | (none) |
| TASK-006 | TASK-001, TASK-002, TASK-003, TASK-004, TASK-005 | TASK-006.1, TASK-006.2, TASK-006.3, TASK-006.4, TASK-006.5, TASK-006.6, TASK-006.7, TASK-006.8, TASK-006.9 |
| TASK-006.1 | TASK-006 | (none) |
| TASK-006.2 | TASK-006 | (none) |
| TASK-006.3 | TASK-006 | (none) |
| TASK-006.4 | TASK-006 | (none) |
| TASK-006.5 | TASK-006 | (none) |
| TASK-006.6 | TASK-006 | (none) |
| TASK-006.7 | TASK-006 | (none) |
| TASK-006.8 | TASK-006 | (none) |
| TASK-006.9 | TASK-006 | (none) |

## Allowed Changes

- Add the skeleton files within this task's target scope (localdatastore/).
- Add the build, wiring and health-check tests under tests/ for 'Local Data Store'.
- Update service registration in the composition root / dependency injection module.
- Add, modify, or remove files within this task's target scope (localdatastore/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Local Data Store'.
- Update service registration in the composition root / dependency injection module where the behaviour needs it.
- Add the skeleton files within this task's target scope (calculationhistory/).
- Add the build, wiring and health-check tests under tests/ for 'Calculation History'.
- Add, modify, or remove files within this task's target scope (calculationhistory/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Calculation History'.
- Add the skeleton files within this task's target scope (errorreporting/).
- Add the build, wiring and health-check tests under tests/ for 'Error Reporting'.
- Add, modify, or remove files within this task's target scope (errorreporting/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Error Reporting'.
- Add the skeleton files within this task's target scope (expressionevaluation/).
- Add the build, wiring and health-check tests under tests/ for 'Expression Evaluation'.
- Add, modify, or remove files within this task's target scope (expressionevaluation/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Expression Evaluation'.
- Add the skeleton files within this task's target scope (roundingandprecision/).
- Add the build, wiring and health-check tests under tests/ for 'Rounding and Precision'.
- Add, modify, or remove files within this task's target scope (roundingandprecision/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Rounding and Precision'.
- Add the skeleton files within this task's target scope (consolehost/).
- Add the build, wiring and health-check tests under tests/ for 'Console Host'.
- Add, modify, or remove files within this task's target scope (consolehost/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Console Host'.

## Prohibited Changes

- Implementing feature or requirement behaviour: that belongs to the sub-tasks of this component.
- Modifying another task's target scope without an explicit, recorded dependency.
- Introducing an unapproved external package, dependency, or architecture style not recorded in the Solution Blueprint.
- Mutating applied database migrations in place - always create a new migration for schema changes.
- Committing hardcoded secrets, API keys, credentials, or environment-specific values.
- Altering or circumventing locked user decisions and governance constraints.
- Transmitting, caching, or routing sensitive or customer data to external regions or unapproved third-party endpoints.
- Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 as a console application, tested with xUnit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file accessed with Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (System.Decimal for arithmetic operations).
- Do not substitute, replace, or alter the locked decision for Technology (Console.ReadLine for user input).
- Do not substitute, replace, or alter the locked decision for Technology (Decimal rounding for results).
- Do not substitute, replace, or alter the locked decision for Technology (Console.Error for error messages).
- Implementing a requirement that belongs to another sub-task of TASK-001 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.2 (Ensure data retention by maintaining the last 10).
- Out of scope (build nothing of): the responsibilities of the other components - Calculation History, Error Reporting, Expression Evaluation, Rounding and Precision, Console Host.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.1 (Maintain a local SQLite database to store the last 10).
- Implementing a requirement that belongs to another sub-task of TASK-002 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.2 (Delete calculation history from the SQLite database).
- Out of scope (build nothing of): the responsibilities of the other components - Local Data Store, Error Reporting, Expression Evaluation, Rounding and Precision, Console Host.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Provide audit logging (+1 related Should requirement)).
- Implementing a requirement that belongs to another sub-task of TASK-003 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-003.2 (Accurately evaluate division operations).
- Out of scope (build nothing of): the responsibilities of the other components - Local Data Store, Calculation History, Expression Evaluation, Rounding and Precision, Console Host.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-003.1 (Provide clear error messages for malformed expressions).
- Implementing a requirement that belongs to another sub-task of TASK-004 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.2 (Evaluate arithmetic expressions quickly enough).
- Out of scope (build nothing of): the responsibilities of the other components - Local Data Store, Calculation History, Error Reporting, Rounding and Precision, Console Host.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Evaluate arithmetic expressions).
- Implementing a requirement that belongs to another sub-task of TASK-005 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.2 (Use decimal arithmetic for all calculations to ensure); TASK-005.3 (All arithmetic operations are performed).
- Out of scope (build nothing of): the responsibilities of the other components - Local Data Store, Calculation History, Error Reporting, Expression Evaluation, Console Host.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.1 (Handle rounding using decimal arithmetic to avoid); TASK-005.3 (All arithmetic operations are performed).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.1 (Handle rounding using decimal arithmetic to avoid); TASK-005.2 (Use decimal arithmetic for all calculations to ensure).
- Implementing a requirement that belongs to another sub-task of TASK-006 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the responsibilities of the other components - Local Data Store, Calculation History, Error Reporting, Expression Evaluation, Rounding and Precision.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.8 (Ensure the command-line calculator provides accurate results); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.9 (Provide built-in help documentation (+2 related Should re...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results).

## Modifiable Paths

- `(proposed) localdatastore/`
- `(proposed) calculationhistory/`
- `(proposed) errorreporting/`
- `(proposed) expressionevaluation/`
- `(proposed) roundingandprecision/`
- `(proposed) consolehost/`

## Prohibited Paths

- `08-commercial/**`
- `.git/**`

## Selected Technology

- **Technology**: C# on .NET 10 as a console application, tested with xUnit (rejected alternatives, do not use: Python 3 script tested with pytest (the team knows .NET; a Python runtime would have to be installed on analyst laptops); F# on .NET 10 (no team experience)). Rationale: Implementation language and test framework. The team already knows C# and .NET, and System.Decimal avoids the binary floating-point errors that are the core problem. The owner mandates .NET for the showcase.
- **Technology**: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (rejected alternatives, do not use: a JSON file rewritten after every calculation (no transactions; a crash mid-write corrupts the history); a plain-text file with one line per calculation (same weakness, and no way to enforce the last-10 rule atomically)). Rationale: Storage for the calculation history. SQLite is the mandated database. It gives transactional writes, survives a crash mid-write, needs no server and is one file to back up or delete.
- **Technology**: System.Decimal for arithmetic operations (rejected alternatives, do not use: double for arithmetic operations). Rationale: System.Decimal is the preferred choice for this project due to its ability to handle financial calculations accurately. The requirement for precise arithmetic evaluation (R10) and the need to avoid floating-point inaccuracies make System.Decimal the only viable option. Switching to double would compromise the integrity of the calculations, which is unacceptable given the project's goals.
- **Technology**: Console.ReadLine for user input (rejected alternatives, do not use: Command-line arguments for user input). Rationale: Both input methods are viable, but Console.ReadLine is preferred for its simplicity and direct interaction with users. Command-line arguments can be considered for advanced use cases where batch processing is needed.
- **Technology**: Decimal rounding for results (rejected alternatives, do not use: String formatting for output). Rationale: Decimal rounding is essential for financial accuracy, while string formatting enhances user experience. Both should be implemented to ensure the calculator meets its functional requirements.
- **Technology**: Console.Error for error messages (rejected alternatives, do not use: Throwing exceptions for error handling). Rationale: Both options provide mechanisms for handling errors gracefully, but using Console.Error aligns with the requirement for clear user feedback without crashing the application.

## Authority Order & Source of Truth

1. **User Mandate / Pinned Baseline**: Absolute authority; cannot be altered or substituted.
2. **Approved Requirements**: Must > Should > Could criteria.
3. **Architecture Decisions & Technology Constraints**: The selected technology stack listed under Selected Technology, plus the patterns defined in the Solution Blueprint.
4. **Task Packet Directives**: Scoped allowed changes, prohibited changes, and acceptance criteria.
5. **Agent Implementation Discretion**: Strictly limited to internal implementation within allowed scope.

## Zero Silent Assumptions & Autonomous Execution Directives

- **No Clarification Questions for Pre-decided Architecture**: The technology decisions listed under Selected Technology are decided and locked. DO NOT prompt the user asking what technology, framework, database, or library to use where one is listed. If a needed choice is not listed there or in the task packet, stop and escalate; never pick a stack yourself.
- **Contradiction & Stop Protocol**: If you encounter an explicit contradiction between task directives, or between a requirement and an architecture decision, DO NOT guess or pick a side. Escalate immediately with the exact conflict and stop.
- **No Scope Creep**: Only edit files matched by `Modifiable Paths` and explicitly referenced in the active task packet.

## Locked Decisions

These decisions are locked. Do not change, replace or work around them; if a task seems to require it, stop and escalate.

- `021ab9627bfe41aa9d543550dffc57d1` **Technology** (technology): Console.Error for error messages
- `245f0843a31d48bcb3bfea5a95f1099a` **Technology** (technology): an embedded SQLite database file accessed with Microsoft.Data.Sqlite
- `6b86061daec44e2d9a7ac0d88388e6c6` **Technology** (technology): C# on .NET 10 as a console application, tested with xUnit
- `ca47ae8c4ad8485ab6351de4376c04c3` **Technology** (technology): Decimal rounding for results
- `d24a599f6c4f4760a7e7251ca0673579` **Technology** (technology): System.Decimal for arithmetic operations
- `efb7f32edda64c679b9b293d2f4af6b3` **Technology** (technology): Console.ReadLine for user input

## Evidence & Reporting Format

When a task is finished, record this report in the task's `checkpointUpdate` notes and in the pull request description:

- **Task**: the task key and title.
- **Status**: `completed`, or `blocked` with the reason.
- **Files changed**: every file added, changed or removed.
- **Commands run**: each command from the task's `commands`, with its result.
- **Tests**: the test that proves each item in the task's `tests` and `definitionOfDone`.
- **Locked decisions**: confirm none was changed (list ids if one was touched; that requires escalation first).
- **Deviations and escalations**: anything done differently from the packet, or escalated, and to whom.

