# TASK-005 — Scaffold Rounding and Precision (LogicalModule)

- **Component:** Rounding and Precision (LogicalModule) · primary task · **Status:** not_started · **Parallel-safe:** Yes
- **Depends on:** TASK-001 · **Unlocks:** TASK-005.1, TASK-005.2, TASK-005.3, TASK-006
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Rounding and Precision' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Rounding and Precision' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Rounding and Precision' skeleton in place.
- Health check test: the module loads and its self-check passes.

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
| `(proposed) roundingandprecision/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (roundingandprecision/). Add the build, wiring and health-check tests under tests/ for 'Rounding and Precision'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Rounding and Precision' (LogicalModule) within the target scope (roundingandprecision/): the empty project or module structure only.
2. Wire 'Rounding and Precision' into the composition root following existing repository conventions.
3. Add the registration entry point for 'Rounding and Precision' and a trivial self-check that proves the module loads.
4. Do not implement any feature behaviour: the sub-tasks of TASK-005 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

- **Data:** Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.

## Quality and Security (this task)
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.; The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.; The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Rounding and Precision (`d60145edd14a4b468fc4a4b1f8caccf4`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
