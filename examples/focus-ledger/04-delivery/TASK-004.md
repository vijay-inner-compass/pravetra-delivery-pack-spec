# TASK-004 — Scaffold Desktop Client (ClientApp)

- **Component:** Desktop Client (ClientApp) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001, TASK-002, TASK-003 · **Unlocks:** TASK-004.1, TASK-004.2, TASK-004.3, TASK-004.4
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Desktop Client' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Desktop Client' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Desktop Client' skeleton in place.
- Health check test: the application starts, shows its window and exits cleanly.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 with the Avalonia UI desktop toolkit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (CSV export).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) desktopclient/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (desktopclient/). Add the build, wiring and health-check tests under tests/ for 'Desktop Client'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Desktop Client' (ClientApp) within the target scope (desktopclient/): the empty project or module structure only.
2. Wire 'Desktop Client' into the composition root following existing repository conventions.
3. Add a minimal main window that opens and closes cleanly, and a startup self-check that reports the application started.
4. Do not implement any feature behaviour: the sub-tasks of TASK-004 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
No network API. The client calls the domain modules in-process; import and export file formats, if any, are recorded here.

- **Data:** Holds transient interface state only; all durable data is read and written through the local data store.

## Quality and Security (this task)
- Architecture decomposition boundary: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems.
• Run the domain modules in-process on the user's machine; no network service is involved.
• Keep window and view state locally; every durable fact goes through the local data store.
- **Source references:** BlueprintComponent: Desktop Client (`9a730da684404e80880bd8ddcf6b6db8`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
