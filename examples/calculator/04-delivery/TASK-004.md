# TASK-004 — Scaffold Expression Evaluation (LogicalModule)

- **Component:** Expression Evaluation (LogicalModule) · primary task · **Status:** not_started · **Parallel-safe:** Yes
- **Depends on:** TASK-001 · **Unlocks:** TASK-004.1, TASK-004.2, TASK-006
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Expression Evaluation' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Expression Evaluation' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Expression Evaluation' skeleton in place.
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
| `(proposed) expressionevaluation/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (expressionevaluation/). Add the build, wiring and health-check tests under tests/ for 'Expression Evaluation'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Expression Evaluation' (LogicalModule) within the target scope (expressionevaluation/): the empty project or module structure only.
2. Wire 'Expression Evaluation' into the composition root following existing repository conventions.
3. Add the registration entry point for 'Expression Evaluation' and a trivial self-check that proves the module loads.
4. Do not implement any feature behaviour: the sub-tasks of TASK-004 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

- **Data:** Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.

## Quality and Security (this task)
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.; The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Expression Evaluation (`92d9f81ac4fc47faa1d55d9950be38e7`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
