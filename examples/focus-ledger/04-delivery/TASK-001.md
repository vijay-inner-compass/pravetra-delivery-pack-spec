# TASK-001 — Scaffold Local Encrypted Database (DataStore)

- **Component:** Local Encrypted Database (DataStore) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** (none) · **Unlocks:** TASK-001.1, TASK-001.2, TASK-001.3, TASK-001.4, TASK-001.5, TASK-002, TASK-003, TASK-004
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Local Encrypted Database' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Local Encrypted Database' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Local Encrypted Database' skeleton in place.
- Health check test: the store can be created empty and a connection check succeeds.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 with the Avalonia UI desktop toolkit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (CSV export).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) localencrypteddatabase/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (localencrypteddatabase/). Add the build, wiring and health-check tests under tests/ for 'Local Encrypted Database'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Local Encrypted Database' (DataStore) within the target scope (localencrypteddatabase/): the empty project or module structure only.
2. Wire 'Local Encrypted Database' into the composition root following existing repository conventions.
3. Add the creation of the empty embedded database file on first run and a connectivity self-check; no tables for features yet.
4. Do not implement any feature behaviour: the sub-tasks of TASK-001 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
Accessed only through the domain modules, in-process, through the embedded database driver; no network access.

- **Data:** Embedded relational schema with versioned local upgrades; the file is created on first run and never leaves the user's machine unless the user exports it.

## Quality and Security (this task)
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Persist the application's data in a single local database file on the user's machine.
• Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store).
• Support backup and restore of the one file, and versioned local schema upgrades when the application is updated.
- **Source references:** BlueprintComponent: Local Encrypted Database (`386f3f2fb8fc44b7ad3c90e6f2d89ddb`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
