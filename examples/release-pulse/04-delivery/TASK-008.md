# TASK-008 — Scaffold Web Client (ClientApp)

- **Component:** Web Client (ClientApp) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007 · **Unlocks:** TASK-008.1, TASK-008.2
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Web Client' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Web Client' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Web Client' skeleton in place.
- Health check test: the client builds and its landing view renders.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) webclient/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (webclient/). Add the build, wiring and health-check tests under tests/ for 'Web Client'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Web Client' (ClientApp) within the target scope (webclient/): the empty project or module structure only.
2. Wire 'Web Client' into the composition root following existing repository conventions.
3. Add a minimal landing view that renders in the browser, and a smoke check that the client builds and loads.
4. Do not implement any feature behaviour: the sub-tasks of TASK-008 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
Consumes HTTPS REST/JSON endpoints with token-based authorization. Handles RFC 7807 problem details and client-side error states.

- **Data:** Client-side reactive state managed in memory and browser storage (session tokens, preferences); no direct database access. Data sensitivity & client-side boundary: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….

## Quality and Security (this task)
- Architecture decomposition boundary: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Provide responsive and accessible user interface for solution workflows.
• Coordinate client-side state management, route transitions, and input validation.
• Manage authentication sessions and handle operational error display.
- **Source references:** BlueprintComponent: Web Client (`5f5e545d708a47798e46101239127eb5`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
