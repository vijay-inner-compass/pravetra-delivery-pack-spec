# TASK-006 — Scaffold Ingest Worker (BackgroundWorker)

- **Component:** Ingest Worker (BackgroundWorker) · primary task · **Status:** not_started · **Parallel-safe:** Yes
- **Depends on:** TASK-001, TASK-002, TASK-003, TASK-004 · **Unlocks:** TASK-006.1, TASK-008
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Ingest Worker' exists as a buildable skeleton, wired into the solution, with a working health check and no feature behaviour; its sub-tasks add the features.

## Done when
- [ ] 'Ingest Worker' builds, is wired into the solution and its health check passes, with no feature behaviour added.

## Tests
- The solution builds with the 'Ingest Worker' skeleton in place.
- Health check test: the health signal reports started once the worker loop runs.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) ingestworker/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add the skeleton files within this task's target scope (ingestworker/). Add the build, wiring and health-check tests under tests/ for 'Ingest Worker'. Update service registration in the composition root / dependency injection module.

## Implementation Steps
1. Scaffold the component boundary for 'Ingest Worker' (BackgroundWorker) within the target scope (ingestworker/): the empty project or module structure only.
2. Wire 'Ingest Worker' into the composition root following existing repository conventions.
3. Add a health signal the platform can probe (a heartbeat or health endpoint) that reports the worker loop has started; the loop itself may be empty.
4. Do not implement any feature behaviour: the sub-tasks of TASK-006 (TASK-nnn.m) deliver it, one unit of functionality each.
5. Run the build and the health check; fix only what stops the skeleton from building or starting.

## Contract
Internal job execution contract (a worker interface in the language of the chosen stack). Triggered via an in-process queue or timer schedule.

- **Data:** Reads/updates job state records in the primary datastore; ensures idempotent task execution.

## Quality and Security (this task)
- Architecture decomposition boundary: Dedicated background processing decouples resource-intensive or long-running tasks from user-facing request latency budgets.

## Current State Evidence
Greenfield component per Solution Blueprint. Target responsibilities:
• Run the ingest worker as its own background process, separate from the API service and the other workers.
• Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting.
• Retry failed items with backoff and record failures in structured logs.
- **Source references:** BlueprintComponent: Ingest Worker (`fcbe7ccd4a3248d6aa247f58e45bb44a`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
