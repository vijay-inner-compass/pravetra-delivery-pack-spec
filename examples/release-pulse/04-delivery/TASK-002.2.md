# TASK-002.2 — Integrate with the CI system to receive deploy

- **Component:** API / Backend Service · sub-task of TASK-002 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-002 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Integrate with the CI system to receive deploy.
> **Requirement:** Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.

## Done when
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.
- Also: Acceptance (negative) for [Must] Integrate with the CI system to receive deploy events in ...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Must] Integrate with the CI system to receive deploy events in ...: Given valid input, when the function described by this requirement is used, then the system does what it states: Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.

## Out of scope
- the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.5 (Implement role-based access control for engineering managers); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- the responsibilities of the other components - Primary Database, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker, Web Client.

## Applicable decisions
- [2e256e04822c45e682a8e122297a8f72] Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process
- [83bdfa6479364845ba31d373b5805387] Technology: a SQLite-backed job table polled by the hosted background services
- [ce1b21ededfb41c2b326791ecc0ae64b] Technology: ASP.NET Core Web API with polling mechanism
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (2 listed), each shown by a named test or check.
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
| `(proposed) apibackendservice/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (apibackendservice/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'API / Backend Service'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-002 builds and its health check passes.
2. Implement: Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Coordinates database transactions across modules; manages connection lifetimes and migration application.
6. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.

## Quality and Security (this task)
- Data handling and retention specification: Coordinates database transactions across modules; manages connection lifetimes and migration application.
- Architecture decomposition boundary: Core deployable boundary hosting API surface and domain logic as a cohesive Hybrid unit, balancing maintainability and deployment simplicity.
- Non-functional target (Ensure the application is available during working hours,...): Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.
- Non-functional target (Process incoming webhook events with a latency of no more...): Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.
- Non-functional target (Implement data encryption in transit and at rest to prote...): Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.
- Non-functional target (Maintain an audit log of all actions taken within the app...): Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.
- Non-functional target (Ensure the application is scalable to handle increased da...): Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.
- Non-functional target (Ensure the application complies with internal data protec...): Ensure the application complies with internal data protection policies, including data retention and access controls.
- Non-functional target (Ensure the application is maintainable, allowing for upda...): Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## Current State Evidence
Builds on the skeleton of 'API / Backend Service' delivered by TASK-002. Greenfield component per Solution Blueprint. Target responsibilities:
• Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Source references:** BlueprintComponent: API / Backend Service (`b90c2b9741d64482a78a525ff6486a05`); Requirement: [Must] Integrate with the CI system to receive deploy (`725c4985365440e884e68f95215b107f`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
