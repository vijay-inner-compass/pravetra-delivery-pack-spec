# TASK-001 — Scaffold Local Data Store (DataStore)

- **Component:** Local Data Store (DataStore) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** (none) · **Unlocks:** TASK-001.1, TASK-001.2, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Local Data Store' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Local Data Store' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Local Data Store' skeleton in place.
- Health check test: the store can be created empty and a connection check succeeds.

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

**Allowed changes:** Add the skeleton files within this task's target scope (localdatastore/). Add the build, wiring and health-check tests under tests/ for 'Local Data Store'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Local Data Store' (DataStore) within the target scope (localdatastore/): the empty project or module structure only.
2. Wire 'Local Data Store' into the composition root following existing repository conventions.
3. Add the empty database bootstrap (the first, empty migration or file creation) and a connectivity check; no tables for features yet.
4. Do not implement any feature behaviour: the sub-tasks of TASK-001 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.

- **Data:** Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own).

## Quality and Security (this task)
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Source references:** BlueprintComponent: Local Data Store (`08b2b1be89c342198780376b886bff61`); TechnologyDecision: Technology: C# on .NET 10 as a console application, tested with xUnit (`6b86061daec44e2d9a7ac0d88388e6c6`); TechnologyDecision: Technology: an embedded SQLite database file accessed with Microsoft.Data.Sqlite (`245f0843a31d48bcb3bfea5a95f1099a`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
