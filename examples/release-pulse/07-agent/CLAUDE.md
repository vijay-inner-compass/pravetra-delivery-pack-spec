# CLAUDE.md — Claude Code Agent Policy

> Canonical policy version: blueprint-v3-tasks-29-4d68dc68
> Generated: 2026-10-09 10:53:27Z
> Project: E02-release-pulse
## Mission

Deliver the 29 tasks in the specified sequence to implement the Solution Blueprint for project 'E02-release-pulse', ensuring that all dependencies are respected and without inventing any architecture, data models, or public contracts beyond what is already recorded.

## Architecture

Modular Monolith with Selected Extracted Services

## Tasks

- TASK-001 - Scaffold Primary Database (DataStore) - not_started - depends on: (none)
  - TASK-001.1 - Ensure the application complies - not_started - depends on: TASK-001
- TASK-002 - Scaffold API / Backend Service (DeployableUnit) - not_started - depends on: TASK-001
  - TASK-002.1 - Surface repeated risky release patterns - not_started - depends on: TASK-002
  - TASK-002.2 - Integrate with the CI system to receive deploy - not_started - depends on: TASK-002
  - TASK-002.3 - Integrate with the incident tracking tool to receive - not_started - depends on: TASK-002
  - TASK-002.4 - Implement data encryption in transit and at rest - not_started - depends on: TASK-002
  - TASK-002.5 - Implement role-based access control for engineering managers - not_started - depends on: TASK-002
  - TASK-002.6 - Ensure the application is scalable (+1 related Should requirement) - not_started - depends on: TASK-002
- TASK-003 - Scaffold Data Quality (LogicalModule) - not_started - depends on: TASK-001, TASK-002
  - TASK-003.1 - Maintain an audit log of all actions taken - not_started - depends on: TASK-003
- TASK-004 - Scaffold Release Health Analytics (LogicalModule) - not_started - depends on: TASK-001, TASK-002
  - TASK-004.1 - Normalize incoming deploy and incident data to ensure - not_started - depends on: TASK-004
  - TASK-004.2 - Calculate a release-health score - not_started - depends on: TASK-004
  - TASK-004.3 - Application provides insights into the release health - not_started - depends on: TASK-004
  - TASK-004.4 - Compare release health scores across different teams - not_started - depends on: TASK-004
- TASK-005 - Scaffold Digest Worker (BackgroundWorker) - not_started - depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - TASK-005.1 - Compile a summary of release health - not_started - depends on: TASK-005
  - TASK-005.2 - Ensure the application is available during working hours - not_started - depends on: TASK-005
  - TASK-005.3 - Provide notifications to on-call engineers - not_started - depends on: TASK-005
- TASK-006 - Scaffold Ingest Worker (BackgroundWorker) - not_started - depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - TASK-006.1 - Process incoming webhook events - not_started - depends on: TASK-006
- TASK-007 - Scaffold Scoring Worker (BackgroundWorker) - not_started - depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - TASK-007.1 - Run the scoring worker as own background process - not_started - depends on: TASK-007
  - TASK-007.2 - Take work - not_started - depends on: TASK-007
  - TASK-007.3 - Retry failed items - not_started - depends on: TASK-007
- TASK-008 - Scaffold Web Client (ClientApp) - not_started - depends on: TASK-001, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007
  - TASK-008.1 - Provide a consistent - not_started - depends on: TASK-008
  - TASK-008.2 - Provide a user interface that allows engineering managers - not_started - depends on: TASK-008

## Task Dependencies

| Task | Depends On | Unlocks |
| --- | --- | --- |
| TASK-001 | (none) | TASK-001.1, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007, TASK-008 |
| TASK-001.1 | TASK-001 | (none) |
| TASK-002 | TASK-001 | TASK-002.1, TASK-002.2, TASK-002.3, TASK-002.4, TASK-002.5, TASK-002.6, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007, TASK-008 |
| TASK-002.1 | TASK-002 | (none) |
| TASK-002.2 | TASK-002 | (none) |
| TASK-002.3 | TASK-002 | (none) |
| TASK-002.4 | TASK-002 | (none) |
| TASK-002.5 | TASK-002 | (none) |
| TASK-002.6 | TASK-002 | (none) |
| TASK-003 | TASK-001, TASK-002 | TASK-003.1, TASK-005, TASK-006, TASK-007, TASK-008 |
| TASK-003.1 | TASK-003 | (none) |
| TASK-004 | TASK-001, TASK-002 | TASK-004.1, TASK-004.2, TASK-004.3, TASK-004.4, TASK-005, TASK-006, TASK-007, TASK-008 |
| TASK-004.1 | TASK-004 | (none) |
| TASK-004.2 | TASK-004 | (none) |
| TASK-004.3 | TASK-004 | (none) |
| TASK-004.4 | TASK-004 | (none) |
| TASK-005 | TASK-001, TASK-002, TASK-003, TASK-004 | TASK-005.1, TASK-005.2, TASK-005.3, TASK-008 |
| TASK-005.1 | TASK-005 | (none) |
| TASK-005.2 | TASK-005 | (none) |
| TASK-005.3 | TASK-005 | (none) |
| TASK-006 | TASK-001, TASK-002, TASK-003, TASK-004 | TASK-006.1, TASK-008 |
| TASK-006.1 | TASK-006 | (none) |
| TASK-007 | TASK-001, TASK-002, TASK-003, TASK-004 | TASK-007.1, TASK-007.2, TASK-007.3, TASK-008 |
| TASK-007.1 | TASK-007 | (none) |
| TASK-007.2 | TASK-007 | (none) |
| TASK-007.3 | TASK-007 | (none) |
| TASK-008 | TASK-001, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007 | TASK-008.1, TASK-008.2 |
| TASK-008.1 | TASK-008 | (none) |
| TASK-008.2 | TASK-008 | (none) |

## Allowed Changes

- Add the skeleton files within this task's target scope (primarydatabase/).
- Add the build, wiring and health-check tests under tests/ for 'Primary Database'.
- Update service registration in the composition root / dependency injection module.
- Add, modify, or remove files within this task's target scope (primarydatabase/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Primary Database'.
- Update service registration in the composition root / dependency injection module where the behaviour needs it.
- Add the skeleton files within this task's target scope (apibackendservice/).
- Add the build, wiring and health-check tests under tests/ for 'API / Backend Service'.
- Add, modify, or remove files within this task's target scope (apibackendservice/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'API / Backend Service'.
- Add the skeleton files within this task's target scope (dataquality/).
- Add the build, wiring and health-check tests under tests/ for 'Data Quality'.
- Add, modify, or remove files within this task's target scope (dataquality/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Data Quality'.
- Add the skeleton files within this task's target scope (releasehealthanalytics/).
- Add the build, wiring and health-check tests under tests/ for 'Release Health Analytics'.
- Add, modify, or remove files within this task's target scope (releasehealthanalytics/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Release Health Analytics'.
- Add the skeleton files within this task's target scope (digestworker/).
- Add the build, wiring and health-check tests under tests/ for 'Digest Worker'.
- Add, modify, or remove files within this task's target scope (digestworker/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Digest Worker'.
- Add the skeleton files within this task's target scope (ingestworker/).
- Add the build, wiring and health-check tests under tests/ for 'Ingest Worker'.
- Add, modify, or remove files within this task's target scope (ingestworker/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Ingest Worker'.
- Add the skeleton files within this task's target scope (scoringworker/).
- Add the build, wiring and health-check tests under tests/ for 'Scoring Worker'.
- Add, modify, or remove files within this task's target scope (scoringworker/) that this responsibility needs.
- Add unit and integration tests under tests/ for this responsibility of 'Scoring Worker'.
- Add the skeleton files within this task's target scope (webclient/).
- Add the build, wiring and health-check tests under tests/ for 'Web Client'.
- Add, modify, or remove files within this task's target scope (webclient/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Web Client'.

## Prohibited Changes

- Implementing feature or requirement behaviour: that belongs to the sub-tasks of this component.
- Modifying another task's target scope without an explicit, recorded dependency.
- Introducing an unapproved external package, dependency, or architecture style not recorded in the Solution Blueprint.
- Mutating applied database migrations in place - always create a new migration for schema changes.
- Committing hardcoded secrets, API keys, credentials, or environment-specific values.
- Altering or circumventing locked user decisions and governance constraints.
- Transmitting, caching, or routing sensitive or customer data to external regions or unapproved third-party endpoints.
- Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).
- Implementing a requirement that belongs to another sub-task of TASK-001 or to another component's task.
- Out of scope (build nothing of): the responsibilities of the other components - API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker, Web Client.
- Implementing a requirement that belongs to another sub-task of TASK-002 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.2 (Integrate with the CI system to receive deploy); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.5 (Implement role-based access control for engineering managers); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker, Web Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.5 (Implement role-based access control for engineering managers); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.2 (Integrate with the CI system to receive deploy); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.5 (Implement role-based access control for engineering managers); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.2 (Integrate with the CI system to receive deploy); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.5 (Implement role-based access control for engineering managers); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.2 (Integrate with the CI system to receive deploy); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.6 (Ensure the application is scalable (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Surface repeated risky release patterns); TASK-002.2 (Integrate with the CI system to receive deploy); TASK-002.3 (Integrate with the incident tracking tool to receive); TASK-002.4 (Implement data encryption in transit and at rest); TASK-002.5 (Implement role-based access control for engineering managers).
- Implementing a requirement that belongs to another sub-task of TASK-003 or to another component's task.
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker, Web Client.
- Implementing a requirement that belongs to another sub-task of TASK-004 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.2 (Calculate a release-health score); TASK-004.3 (Application provides insights into the release health); TASK-004.4 (Compare release health scores across different teams).
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Digest Worker, Ingest Worker, Scoring Worker, Web Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Normalize incoming deploy and incident data to ensure); TASK-004.3 (Application provides insights into the release health); TASK-004.4 (Compare release health scores across different teams).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Normalize incoming deploy and incident data to ensure); TASK-004.2 (Calculate a release-health score); TASK-004.4 (Compare release health scores across different teams).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Normalize incoming deploy and incident data to ensure); TASK-004.2 (Calculate a release-health score); TASK-004.3 (Application provides insights into the release health).
- Implementing a requirement that belongs to another sub-task of TASK-005 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.2 (Ensure the application is available during working hours); TASK-005.3 (Provide notifications to on-call engineers).
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Ingest Worker, Scoring Worker, Web Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.1 (Compile a summary of release health); TASK-005.3 (Provide notifications to on-call engineers).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-005.1 (Compile a summary of release health); TASK-005.2 (Ensure the application is available during working hours).
- Implementing a requirement that belongs to another sub-task of TASK-006 or to another component's task.
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Scoring Worker, Web Client.
- Implementing a responsibility or requirement that belongs to another sub-task of TASK-007 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-007.2 (Take work); TASK-007.3 (Retry failed items).
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Web Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-007.1 (Run the scoring worker as own background process); TASK-007.3 (Retry failed items).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-007.1 (Run the scoring worker as own background process); TASK-007.2 (Take work).
- Implementing a requirement that belongs to another sub-task of TASK-008 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-008.2 (Provide a user interface that allows engineering managers).
- Out of scope (build nothing of): the responsibilities of the other components - Primary Database, API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-008.1 (Provide a consistent).

## Modifiable Paths

- `(proposed) primarydatabase/`
- `(proposed) apibackendservice/`
- `(proposed) dataquality/`
- `(proposed) releasehealthanalytics/`
- `(proposed) digestworker/`
- `(proposed) ingestworker/`
- `(proposed) scoringworker/`
- `(proposed) webclient/`

## Prohibited Paths

- `08-commercial/**`
- `.git/**`

## Selected Technology

- **Technology**: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (rejected alternatives, do not use: Python workers beside a .NET API (a second runtime to build, deploy and monitor); Three separate .NET worker processes (three deployments for one small team group)). Rationale: Server language, framework and hosting model. The owner mandates .NET. One process keeps deployment to a single published build, and hosted services give the workers a lifetime tied to the API host without a second runtime.
- **Technology**: a SQLite-backed job table polled by the hosted background services (rejected alternatives, do not use: an in-process channel (System.Threading.Channels) inside the API host (events queued in memory are lost when the host restarts); a spool folder of JSON files read by the workers (no transactions; a crash can lose or double-process an event)). Rationale: Database and background-work queue. SQLite is the mandated database. A job table written in the same transaction as the event makes the at-least-once, scored-once requirement testable, with no broker to run. Write-ahead mode lets the API read while a worker writes.
- **Technology**: ASP.NET Core Web API with polling mechanism (rejected alternatives, do not use: ASP.NET Core Web API with SignalR). Rationale: The choice between SignalR and polling hinges on the need for real-time updates versus simplicity. SignalR offers a more responsive user experience, which aligns with the requirement for timely insights, but comes with added complexity. Polling is easier to implement but may not meet the latency requirements effectively.

## Authority Order & Source of Truth

1. **User Mandate / Pinned Baseline**: Absolute authority; cannot be altered or substituted.
2. **Approved Requirements**: Must > Should > Could criteria.
3. **Architecture Decisions & Technology Constraints**: The selected technology stack listed under Selected Technology, plus the patterns defined in the Solution Blueprint.
4. **Task Packet Directives**: Scoped allowed changes, prohibited changes, and acceptance criteria.
5. **Agent Implementation Discretion**: Strictly limited to internal implementation within allowed scope.

## Zero Silent Assumptions & Autonomous Execution Directives

- **No Clarification Questions for Pre-decided Architecture**: The technology decisions listed under Selected Technology are decided and locked. DO NOT prompt the user asking what technology, framework, database, or library to use where one is listed. If a needed choice is not listed there or in the task packet, stop and escalate; never pick a stack yourself.
- **Contradiction & Stop Protocol**: If you encounter an explicit contradiction between task directives, or between a requirement and an architecture decision, DO NOT guess or pick a side. Escalate immediately with the exact conflict and stop.
- **No Scope Creep**: Only edit files matched by `Modifiable Paths` and explicitly referenced in the active task packet.

## Locked Decisions

These decisions are locked. Do not change, replace or work around them; if a task seems to require it, stop and escalate.

- `2e256e04822c45e682a8e122297a8f72` **Technology** (technology): C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process
- `83bdfa6479364845ba31d373b5805387` **Technology** (technology): a SQLite-backed job table polled by the hosted background services
- `ce1b21ededfb41c2b326791ecc0ae64b` **Technology** (technology): ASP.NET Core Web API with polling mechanism

## Evidence & Reporting Format

When a task is finished, record this report in the task's `checkpointUpdate` notes and in the pull request description:

- **Task**: the task key and title.
- **Status**: `completed`, or `blocked` with the reason.
- **Files changed**: every file added, changed or removed.
- **Commands run**: each command from the task's `commands`, with its result.
- **Tests**: the test that proves each item in the task's `tests` and `definitionOfDone`.
- **Locked decisions**: confirm none was changed (list ids if one was touched; that requires escalation first).
- **Deviations and escalations**: anything done differently from the packet, or escalated, and to whom.


## Skills

- `.claude/skills/domain-terminology.md` — Domain & Terminology
- `.claude/skills/architecture-boundaries.md` — Architecture Boundaries
- `.claude/skills/coding-conventions.md` — Coding Conventions
- `.claude/skills/security-secrets.md` — Security & Secrets
- `.claude/skills/data-migrations.md` — Data & Migrations
- `.claude/skills/testing-validation.md` — Testing & Validation
- `.claude/skills/cicd-branching.md` — CI/CD & Branching
- `.claude/skills/observability.md` — Observability
- `.claude/skills/documentation-traceability.md` — Documentation & Traceability
- `.claude/skills/human-approval-prohibited-actions.md` — Human Approval & Prohibited Actions
