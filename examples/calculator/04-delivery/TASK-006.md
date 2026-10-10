# TASK-006 — Scaffold Console Host (DeployableUnit)

- **Component:** Console Host (DeployableUnit) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001, TASK-002, TASK-003, TASK-004, TASK-005 · **Unlocks:** TASK-006.1, TASK-006.2, TASK-006.3, TASK-006.4, TASK-006.5, TASK-006.6, TASK-006.7, TASK-006.8, TASK-006.9
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Console Host' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Console Host' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Console Host' skeleton in place.
- Health check test: the health check reports success after startup and failure when a required dependency is unreachable.

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

**Allowed changes:** Add the skeleton files within this task's target scope (consolehost/). Add the build, wiring and health-check tests under tests/ for 'Console Host'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Console Host' (DeployableUnit) within the target scope (consolehost/): the empty project or module structure only.
2. Wire 'Console Host' into the composition root following existing repository conventions.
3. Add a health command (for example `--health`) that exits 0 when the tool starts and its configuration loads.
4. Do not implement any feature behaviour: the sub-tasks of TASK-006 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.

- **Data:** Coordinates database transactions across modules; manages connection lifetimes and migration application.

## Quality and Security (this task)
- Architecture decomposition boundary: Core deployable boundary hosting API surface and domain logic as a cohesive ModularMonolith unit, balancing maintainability and deployment simplicity.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Source references:** BlueprintComponent: Console Host (`d8260f5a775848888fbc77db937908c7`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
