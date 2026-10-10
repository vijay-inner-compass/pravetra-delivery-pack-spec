# TASK-002 — Scaffold Session Tracking (LogicalModule)

- **Component:** Session Tracking (LogicalModule) · primary task · **Status:** not_started · **Parallel-safe:** Yes
- **Depends on:** TASK-001 · **Unlocks:** TASK-002.1, TASK-002.2, TASK-002.3, TASK-002.4, TASK-002.5, TASK-002.6, TASK-002.7, TASK-002.8, TASK-004
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Session Tracking' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Session Tracking' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Session Tracking' skeleton in place.
- Health check test: the module loads and its self-check passes.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 with the Avalonia UI desktop toolkit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (CSV export).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) sessiontracking/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (sessiontracking/). Add the build, wiring and health-check tests under tests/ for 'Session Tracking'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Session Tracking' (LogicalModule) within the target scope (sessiontracking/): the empty project or module structure only.
2. Wire 'Session Tracking' into the composition root following existing repository conventions.
3. Add the registration entry point for 'Session Tracking' and a trivial self-check that proves the module loads.
4. Do not implement any feature behaviour: the sub-tasks of TASK-002 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

- **Data:** Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.

## Quality and Security (this task)
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Session Tracking (`10abc4b7178f40a8aa5248ba6e52061d`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
