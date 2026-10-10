# TASK-001 — Scaffold Primary Database (DataStore)

- **Component:** Primary Database (DataStore) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** (none) · **Unlocks:** TASK-001.1, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007, TASK-008
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Primary Database' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Primary Database' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Primary Database' skeleton in place.
- Health check test: the store can be created empty and a connection check succeeds.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) primarydatabase/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (primarydatabase/). Add the build, wiring and health-check tests under tests/ for 'Primary Database'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Primary Database' (DataStore) within the target scope (primarydatabase/): the empty project or module structure only.
2. Wire 'Primary Database' into the composition root following existing repository conventions.
3. Add the empty database bootstrap (the first, empty migration or file creation) and a connectivity check; no tables for features yet.
4. Do not implement any feature behaviour: the sub-tasks of TASK-001 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.

- **Data:** Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). Data lifecycle and residency policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….

## Quality and Security (this task)
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Source references:** BlueprintComponent: Primary Database (`fb295674ebc14ea29a0f9352f6066749`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
