# TASK-006.9 — Provide built-in help documentation (+2 related Should requirements)

- **Component:** Console Host · sub-task of TASK-006 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-006 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Provide built-in help documentation accessible from the terminal.
> **Requirement:** The calculator shall provide built-in help documentation accessible from the terminal.
> **Requirement:** Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.
> **Requirement:** The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.

## Done when
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide built-in help documentation accessible from the terminal.
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.
- [ ] Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide built-in help documentation accessible from the terminal.
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- positive case: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.
- positive case: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
- Also: Acceptance (positive) for [Should] The calculator shall provide built-in help documentation ...: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide built-in help documentation accessible from the terminal.
- Also: Acceptance (negative) for [Should] The calculator shall provide built-in help documentation ...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Should] Ensure that the command-line calculator is user-friendly ...: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.
- Also: Acceptance (positive) for [Should] The calculator shall be maintainable with a low operation...: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.

## Out of scope
- the other sub-tasks of this component - TASK-006.1 (Reduce the error rate in invoice total calculations); TASK-006.2 (Minimize rework time associated); TASK-006.3 (Run locally on each analyst's laptop); TASK-006.4 (Available to analysts whenever they work); TASK-006.5 (Input arithmetic expressions directly into the terminal); TASK-006.6 (Ensure the command-line calculator is compatible); TASK-006.7 (Ensure compliance with internal data handling policies); TASK-006.8 (Ensure the command-line calculator provides accurate results).
- the responsibilities of the other components - Local Data Store, Calculation History, Error Reporting, Expression Evaluation, Rounding and Precision.

## Applicable decisions
- [6b86061daec44e2d9a7ac0d88388e6c6] Technology: C# on .NET 10 as a console application, tested with xUnit
- [245f0843a31d48bcb3bfea5a95f1099a] Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite
- [d24a599f6c4f4760a7e7251ca0673579] Technology: System.Decimal for arithmetic operations
- [efb7f32edda64c679b9b293d2f4af6b3] Technology: Console.ReadLine for user input
- [ca47ae8c4ad8485ab6351de4376c04c3] Technology: Decimal rounding for results
- [021ab9627bfe41aa9d543550dffc57d1] Technology: Console.Error for error messages
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (4 listed), each shown by a named test or check.
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
| `(proposed) consolehost/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (consolehost/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Console Host'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-006 builds and its health check passes.
2. Implement: The calculator shall provide built-in help documentation accessible from the terminal.
3. Implement: Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.
4. Implement: The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
5. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
6. Align the component interface with its contract: (see Contract)
7. Keep to the component's data design: Coordinates database transactions across modules; manages connection lifetimes and migration application.
8. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.

## Quality and Security (this task)
- Data handling and retention specification: Coordinates database transactions across modules; manages connection lifetimes and migration application.
- Architecture decomposition boundary: Core deployable boundary hosting API surface and domain logic as a cohesive ModularMonolith unit, balancing maintainability and deployment simplicity.
- Non-functional target (The calculator shall evaluate arithmetic expressions quic...): The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.
- Non-functional target (The calculator shall be available to analysts whenever th...): The calculator shall be available to analysts whenever they work, because it runs locally on their laptop and needs no network or external service.
- Non-functional target (The calculator shall use decimal arithmetic for all calcu...): The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.
- Non-functional target (The calculator shall provide audit logging of all calcula...): The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.
- Non-functional target (The calculator shall ensure data retention by maintaining...): The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database.
- Non-functional target (The calculator shall be maintainable with a low operation...): The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
- Non-functional target (The calculator shall ensure compliance with internal data...): The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.
- Non-functional target (The calculator shall ensure that all arithmetic operation...): The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.

## Current State Evidence
Builds on the skeleton of 'Console Host' delivered by TASK-006. Greenfield component per Solution Blueprint. Target responsibilities:
• Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Source references:** BlueprintComponent: Console Host (`d8260f5a775848888fbc77db937908c7`); Requirement: [Should] Provide built-in help documentation accessible from the terminal (`2b37f62e18824c729f2151070bdf07bb`); Requirement: [Should] Command-line calculator is user-friendly and requires minimal training (`a227e9b14b204906b9da79ef9fa09252`); Requirement: [Should] Maintainable with a low operational cost (`db5d3811e5574fea9b6cca8537ed88f2`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
