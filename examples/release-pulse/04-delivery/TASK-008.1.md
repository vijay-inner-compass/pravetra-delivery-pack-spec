# TASK-008.1 — Provide a consistent

- **Component:** Web Client · sub-task of TASK-008 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-008 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Provide a consistent, trustworthy weekly release-health view.
> **Requirement:** Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.

## Done when
- [ ] Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.
- negative case: invalid, unauthorised or malformed input for this behaviour is rejected with a clear error.
- Also: Acceptance (positive) for [Must] Provide a consistent, trustworthy weekly release-health v...: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.

## Out of scope
- the other sub-tasks of this component - TASK-008.2 (Provide a user interface that allows engineering managers).
- the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker.

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
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) webclient/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (webclient/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Web Client'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-008 builds and its health check passes.
2. Implement: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Client-side reactive state managed in memory and browser storage (session tokens, preferences); no direct database access. Data sensitivity & client-side boundary: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….

## Contract
Consumes HTTPS REST/JSON endpoints with token-based authorization. Handles RFC 7807 problem details and client-side error states.

## Quality and Security (this task)
- Data handling and retention specification: Client-side reactive state managed in memory and browser storage (session tokens, preferences); no direct database access. Data sensitivity & client-side boundary: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….
- Architecture decomposition boundary: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.
- Non-functional target (Ensure the application is available during working hours,...): Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.
- Non-functional target (Process incoming webhook events with a latency of no more...): Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.
- Non-functional target (Implement data encryption in transit and at rest to prote...): Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.
- Non-functional target (Maintain an audit log of all actions taken within the app...): Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.
- Non-functional target (Ensure the application is scalable to handle increased da...): Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.
- Non-functional target (Ensure the application complies with internal data protec...): Ensure the application complies with internal data protection policies, including data retention and access controls.
- Non-functional target (Ensure the application is maintainable, allowing for upda...): Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## Current State Evidence
Builds on the skeleton of 'Web Client' delivered by TASK-008. Greenfield component per Solution Blueprint. Target responsibilities:
• Provide responsive and accessible user interface for solution workflows.
• Coordinate client-side state management, route transitions, and input validation.
• Manage authentication sessions and handle operational error display.
- **Source references:** BlueprintComponent: Web Client (`5f5e545d708a47798e46101239127eb5`); Requirement: [Must] Provide a consistent (`85c814013bfe4b899485df402472c101`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
