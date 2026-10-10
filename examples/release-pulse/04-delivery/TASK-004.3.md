# TASK-004.3 — Application provides insights into the release health

- **Component:** Release Health Analytics · sub-task of TASK-004 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-004 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Application provides insights into the release health.
> **Requirement:** Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.

## Done when
- [ ] Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.
- negative case: invalid, unauthorised or malformed input for this behaviour is rejected with a clear error.
- Also: Acceptance (positive) for [Must] Ensure that the application provides insights into the re...: Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.

## Out of scope
- the other sub-tasks of this component - TASK-004.1 (Normalize incoming deploy and incident data to ensure); TASK-004.2 (Calculate a release-health score); TASK-004.4 (Compare release health scores across different teams).
- the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Digest Worker, Ingest Worker, Scoring Worker, Web Client.

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
| `(proposed) releasehealthanalytics/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (releasehealthanalytics/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Release Health Analytics'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-004 builds and its health check passes.
2. Implement: Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

## Quality and Security (this task)
- Data handling and retention specification: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.
- Non-functional target (Ensure the application is available during working hours,...): Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.
- Non-functional target (Process incoming webhook events with a latency of no more...): Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.
- Non-functional target (Implement data encryption in transit and at rest to prote...): Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.
- Non-functional target (Maintain an audit log of all actions taken within the app...): Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.
- Non-functional target (Ensure the application is scalable to handle increased da...): Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.
- Non-functional target (Ensure the application complies with internal data protec...): Ensure the application complies with internal data protection policies, including data retention and access controls.
- Non-functional target (Ensure the application is maintainable, allowing for upda...): Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## Current State Evidence
Builds on the skeleton of 'Release Health Analytics' delivered by TASK-004. Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Release Health Analytics (`aef088193f4143caae0c1c1116d456a7`); Requirement: [Must] Application provides insights into the release health (`b31f0c1104d84dc9a80b5ec4cf3862ca`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
