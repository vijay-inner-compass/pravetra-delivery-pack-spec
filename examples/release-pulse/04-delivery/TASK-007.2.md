# TASK-007.2 — Take work

- **Component:** Scoring Worker · sub-task of TASK-007 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-007 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
'Scoring Worker' delivers one of its recorded responsibilities: Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting Done when it is satisfied and the tests pass.

## Done when
- [ ] 'Scoring Worker' satisfies this recorded responsibility - Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting - shown by passing automated tests that name it.

## Write these tests first
- positive case: Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting
- negative case: invalid, unauthorised or malformed input for this behaviour is rejected with a clear error.

## Out of scope
- the other sub-tasks of this component - TASK-007.1 (Run the scoring worker as own background process); TASK-007.3 (Retry failed items).
- the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Web Client.

## Applicable decisions
- [2e256e04822c45e682a8e122297a8f72] Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process
- [83bdfa6479364845ba31d373b5805387] Technology: a SQLite-backed job table polled by the hosted background services
- [ce1b21ededfb41c2b326791ecc0ae64b] Technology: ASP.NET Core Web API with polling mechanism
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (1 listed), each shown by a named test or check.
- [ ] Every test under "Write these tests first" exists, failed before the change, and passes now.
- [ ] The applicable decisions and the common rules are respected and nothing contradicts them.
- [ ] The out-of-scope items are untouched.
- [ ] No unrelated changes: the diff stays inside the allowed paths and only this sub-task's behaviour changed.

## Prohibited (this task)
- Implementing a responsibility or requirement that belongs to another sub-task of TASK-007 or to another component's task.
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) scoringworker/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (scoringworker/) that this responsibility needs. Add unit and integration tests under tests/ for this responsibility of 'Scoring Worker'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-007 builds and its health check passes.
2. Responsibility-derived: no requirement was assigned to 'Scoring Worker', so this sub-task is built from responsibility 2 of 3 recorded for it in the Solution Blueprint; add or trace requirements to this component to replace it with requirement-backed sub-tasks.
3. Implement responsibility: Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Reads/updates job state records in the primary datastore; ensures idempotent task execution.

## Contract
Internal job execution contract (a worker interface in the language of the chosen stack). Triggered via an in-process queue or timer schedule.

## Quality and Security (this task)
- Data handling and retention specification: Reads/updates job state records in the primary datastore; ensures idempotent task execution.
- Architecture decomposition boundary: Dedicated background processing decouples resource-intensive or long-running tasks from user-facing request latency budgets.
- Responsibility-derived: no requirement was assigned to 'Scoring Worker', so this sub-task is built from responsibility 2 of 3 recorded for it in the Solution Blueprint; add or trace requirements to this component to replace it with requirement-backed sub-tasks.
- Non-functional target (Ensure the application is available during working hours,...): Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.
- Non-functional target (Process incoming webhook events with a latency of no more...): Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.
- Non-functional target (Implement data encryption in transit and at rest to prote...): Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.
- Non-functional target (Maintain an audit log of all actions taken within the app...): Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.
- Non-functional target (Ensure the application is scalable to handle increased da...): Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.
- Non-functional target (Ensure the application complies with internal data protec...): Ensure the application complies with internal data protection policies, including data retention and access controls.
- Non-functional target (Ensure the application is maintainable, allowing for upda...): Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## Current State Evidence
Builds on the skeleton of 'Scoring Worker' delivered by TASK-007. Greenfield component per Solution Blueprint. Target responsibilities:
• Run the scoring worker as its own background process, separate from the API service and the other workers.
• Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting.
• Retry failed items with backoff and record failures in structured logs.
- **Source references:** BlueprintComponent: Scoring Worker (`13d1dd3ca85b4f21ab6ba834f8c7b8e5`); ComponentResponsibility: Responsibility 2 of 3: Take its work from the durable queue or schedule recorded in the technology a... (`13d1dd3ca85b4f21ab6ba834f8c7b8e5#2`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
