# TASK-003.1 — Provide clear error messages for malformed expressions

- **Component:** Error Reporting · sub-task of TASK-003 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-003 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.
> **Requirement:** The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.

## Done when
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.
- Also: Acceptance (negative) for [Must] The calculator shall provide clear error messages for mal...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Must] The calculator shall provide clear error messages for mal...: Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.

## Out of scope
- the other sub-tasks of this component - TASK-003.2 (Accurately evaluate division operations).
- the responsibilities of the other components - Local Data Store, Calculation History, Expression Evaluation, Rounding and Precision, Console Host.

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
| `(proposed) errorreporting/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (errorreporting/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Error Reporting'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-003 builds and its health check passes.
2. Implement: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
6. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

## Quality and Security (this task)
- Data handling and retention specification: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.
- Non-functional target (The calculator shall evaluate arithmetic expressions quic...): The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.
- Non-functional target (The calculator shall be available to analysts whenever th...): The calculator shall be available to analysts whenever they work, because it runs locally on their laptop and needs no network or external service.
- Non-functional target (The calculator shall use decimal arithmetic for all calcu...): The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.
- Non-functional target (The calculator shall provide audit logging of all calcula...): The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.
- Non-functional target (The calculator shall ensure data retention by maintaining...): The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database.
- Non-functional target (The calculator shall be maintainable with a low operation...): The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.
- Non-functional target (The calculator shall ensure compliance with internal data...): The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.
- Non-functional target (The calculator shall ensure that all arithmetic operation...): The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.

## Current State Evidence
Builds on the skeleton of 'Error Reporting' delivered by TASK-003. Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.; The calculator shall accurately evaluate division operations, including handling division by zero gracefully..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Error Reporting (`5d96b4613df04692aa691e5465528e63`); Requirement: [Must] Provide clear error messages for malformed expressions (`50584c0166234f68809ca067377e924e`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
