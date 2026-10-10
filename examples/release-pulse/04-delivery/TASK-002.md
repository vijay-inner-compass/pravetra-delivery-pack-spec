# TASK-002 — Scaffold API / Backend Service (DeployableUnit)

- **Component:** API / Backend Service (DeployableUnit) · primary task · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001 · **Unlocks:** TASK-002.1, TASK-002.2, TASK-002.3, TASK-002.4, TASK-002.5, TASK-002.6, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007, TASK-008
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'API / Backend Service' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'API / Backend Service' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'API / Backend Service' skeleton in place.
- Health check test: the health check reports success after startup and failure when a required dependency is unreachable.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) apibackendservice/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (apibackendservice/). Add the build, wiring and health-check tests under tests/ for 'API / Backend Service'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'API / Backend Service' (DeployableUnit) within the target scope (apibackendservice/): the empty project or module structure only.
2. Wire 'API / Backend Service' into the composition root following existing repository conventions.
3. Add a health check endpoint (for example GET /health) that reports success once the service has started and its dependencies are reachable.
4. Do not implement any feature behaviour: the sub-tasks of TASK-002 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.

- **Data:** Coordinates database transactions across modules; manages connection lifetimes and migration application.

## Quality and Security (this task)
- Architecture decomposition boundary: Core deployable boundary hosting API surface and domain logic as a cohesive Hybrid unit, balancing maintainability and deployment simplicity.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Source references:** BlueprintComponent: API / Backend Service (`b90c2b9741d64482a78a525ff6486a05`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
