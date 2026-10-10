# OpenCode Agent Conventions

> Canonical policy version: blueprint-v2-tasks-23-15bea665
> Generated: 2026-10-09 11:48:57Z
> Project: E03-focus-ledger
## Mission

Deliver the 23 tasks in the specified dependency order to implement the Solution Blueprint for project 'E03-focus-ledger', adhering strictly to the recorded architecture style of Modular Monolith, without inventing any architecture, data models, or public contracts.

## Architecture

Modular Monolith

## Tasks

- TASK-001 - Scaffold Local Encrypted Database (DataStore) - not_started - depends on: (none)
  - TASK-001.1 - Store all session data - not_started - depends on: TASK-001
  - TASK-001.2 - Encrypt all stored data at rest using AES-256 encryption - not_started - depends on: TASK-001
  - TASK-001.3 - Provide a backup and recovery mechanism that allows users - not_started - depends on: TASK-001
  - TASK-001.4 - Comply with GDPR regulations - not_started - depends on: TASK-001
  - TASK-001.5 - Edit or delete past focus sessions - not_started - depends on: TASK-001
- TASK-002 - Scaffold Session Tracking (LogicalModule) - not_started - depends on: TASK-001
  - TASK-002.1 - Accurately track billable hours - not_started - depends on: TASK-002
  - TASK-002.2 - Start a focus session by selecting a client and entering - not_started - depends on: TASK-002
  - TASK-002.3 - Prompt the user - not_started - depends on: TASK-002
  - TASK-002.4 - Timer updates in real-time - not_started - depends on: TASK-002
  - TASK-002.5 - Start and record focus sessions - not_started - depends on: TASK-002
  - TASK-002.6 - Manually stop a focus session and record the end time - not_started - depends on: TASK-002
  - TASK-002.7 - Session data is backed up at least once a week to prevent - not_started - depends on: TASK-002
  - TASK-002.8 - Access historical session data (+1 related Should requirement) - not_started - depends on: TASK-002
- TASK-003 - Scaffold Timesheet and Export (LogicalModule) - not_started - depends on: TASK-001
  - TASK-003.1 - Provide users with a trustworthy weekly timesheet - not_started - depends on: TASK-003
  - TASK-003.2 - Export timesheet as a CSV or PDF file - not_started - depends on: TASK-003
- TASK-004 - Scaffold Desktop Client (ClientApp) - not_started - depends on: TASK-001, TASK-002, TASK-003
  - TASK-004.1 - Display a timer in the system tray that counts the duration - not_started - depends on: TASK-004
  - TASK-004.2 - Provide a weekly review screen that totals sessions - not_started - depends on: TASK-004
  - TASK-004.3 - View a history of past focus sessions - not_started - depends on: TASK-004
  - TASK-004.4 - Have a user interface that adheres (+1 related Should requirement) - not_started - depends on: TASK-004

## Task Dependencies

| Task | Depends On | Unlocks |
| --- | --- | --- |
| TASK-001 | (none) | TASK-001.1, TASK-001.2, TASK-001.3, TASK-001.4, TASK-001.5, TASK-002, TASK-003, TASK-004 |
| TASK-001.1 | TASK-001 | (none) |
| TASK-001.2 | TASK-001 | (none) |
| TASK-001.3 | TASK-001 | (none) |
| TASK-001.4 | TASK-001 | (none) |
| TASK-001.5 | TASK-001 | (none) |
| TASK-002 | TASK-001 | TASK-002.1, TASK-002.2, TASK-002.3, TASK-002.4, TASK-002.5, TASK-002.6, TASK-002.7, TASK-002.8, TASK-004 |
| TASK-002.1 | TASK-002 | (none) |
| TASK-002.2 | TASK-002 | (none) |
| TASK-002.3 | TASK-002 | (none) |
| TASK-002.4 | TASK-002 | (none) |
| TASK-002.5 | TASK-002 | (none) |
| TASK-002.6 | TASK-002 | (none) |
| TASK-002.7 | TASK-002 | (none) |
| TASK-002.8 | TASK-002 | (none) |
| TASK-003 | TASK-001 | TASK-003.1, TASK-003.2, TASK-004 |
| TASK-003.1 | TASK-003 | (none) |
| TASK-003.2 | TASK-003 | (none) |
| TASK-004 | TASK-001, TASK-002, TASK-003 | TASK-004.1, TASK-004.2, TASK-004.3, TASK-004.4 |
| TASK-004.1 | TASK-004 | (none) |
| TASK-004.2 | TASK-004 | (none) |
| TASK-004.3 | TASK-004 | (none) |
| TASK-004.4 | TASK-004 | (none) |

## Allowed Changes

- Add the skeleton files within this task's target scope (localencrypteddatabase/).
- Add the build, wiring and health-check tests under tests/ for 'Local Encrypted Database'.
- Update service registration in the composition root / dependency injection module.
- Add, modify, or remove files within this task's target scope (localencrypteddatabase/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Local Encrypted Database'.
- Update service registration in the composition root / dependency injection module where the behaviour needs it.
- Add the skeleton files within this task's target scope (sessiontracking/).
- Add the build, wiring and health-check tests under tests/ for 'Session Tracking'.
- Add, modify, or remove files within this task's target scope (sessiontracking/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Session Tracking'.
- Add the skeleton files within this task's target scope (timesheetandexport/).
- Add the build, wiring and health-check tests under tests/ for 'Timesheet and Export'.
- Add, modify, or remove files within this task's target scope (timesheetandexport/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Timesheet and Export'.
- Add the skeleton files within this task's target scope (desktopclient/).
- Add the build, wiring and health-check tests under tests/ for 'Desktop Client'.
- Add, modify, or remove files within this task's target scope (desktopclient/) that this requirement needs.
- Add unit and integration tests under tests/ for this requirement of 'Desktop Client'.

## Prohibited Changes

- Implementing feature or requirement behaviour: that belongs to the sub-tasks of this component.
- Modifying another task's target scope without an explicit, recorded dependency.
- Introducing an unapproved external package, dependency, or architecture style not recorded in the Solution Blueprint.
- Mutating applied database migrations in place - always create a new migration for schema changes.
- Committing hardcoded secrets, API keys, credentials, or environment-specific values.
- Altering or circumventing locked user decisions and governance constraints.
- Persisting unmasked PII, credentials, or sensitive data in server logs or unencrypted data stores.
- Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 with the Avalonia UI desktop toolkit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (CSV export).
- Implementing a requirement that belongs to another sub-task of TASK-001 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.2 (Encrypt all stored data at rest using AES-256 encryption); TASK-001.3 (Provide a backup and recovery mechanism that allows users); TASK-001.4 (Comply with GDPR regulations); TASK-001.5 (Edit or delete past focus sessions).
- Out of scope (build nothing of): the responsibilities of the other components - Session Tracking, Timesheet and Export, Desktop Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.1 (Store all session data); TASK-001.3 (Provide a backup and recovery mechanism that allows users); TASK-001.4 (Comply with GDPR regulations); TASK-001.5 (Edit or delete past focus sessions).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.1 (Store all session data); TASK-001.2 (Encrypt all stored data at rest using AES-256 encryption); TASK-001.4 (Comply with GDPR regulations); TASK-001.5 (Edit or delete past focus sessions).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.1 (Store all session data); TASK-001.2 (Encrypt all stored data at rest using AES-256 encryption); TASK-001.3 (Provide a backup and recovery mechanism that allows users); TASK-001.5 (Edit or delete past focus sessions).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-001.1 (Store all session data); TASK-001.2 (Encrypt all stored data at rest using AES-256 encryption); TASK-001.3 (Provide a backup and recovery mechanism that allows users); TASK-001.4 (Comply with GDPR regulations).
- Implementing a requirement that belongs to another sub-task of TASK-002 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the responsibilities of the other components - Local Encrypted Database, Timesheet and Export, Desktop Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.8 (Access historical session data (+1 related Should require...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.2 (Start a focus session by selecting a client and entering); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent).
- Implementing a requirement that belongs to another sub-task of TASK-003 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-003.2 (Export timesheet as a CSV or PDF file).
- Out of scope (build nothing of): the responsibilities of the other components - Local Encrypted Database, Session Tracking, Desktop Client.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-003.1 (Provide users with a trustworthy weekly timesheet).
- Implementing a requirement that belongs to another sub-task of TASK-004 or to another component's task.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.2 (Provide a weekly review screen that totals sessions); TASK-004.3 (View a history of past focus sessions); TASK-004.4 (Have a user interface that adheres (+1 related Should req...).
- Out of scope (build nothing of): the responsibilities of the other components - Local Encrypted Database, Session Tracking, Timesheet and Export.
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Display a timer in the system tray that counts the duration); TASK-004.3 (View a history of past focus sessions); TASK-004.4 (Have a user interface that adheres (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Display a timer in the system tray that counts the duration); TASK-004.2 (Provide a weekly review screen that totals sessions); TASK-004.4 (Have a user interface that adheres (+1 related Should req...).
- Out of scope (build nothing of): the other sub-tasks of this component - TASK-004.1 (Display a timer in the system tray that counts the duration); TASK-004.2 (Provide a weekly review screen that totals sessions); TASK-004.3 (View a history of past focus sessions).

## Modifiable Paths

- `(proposed) localencrypteddatabase/`
- `(proposed) sessiontracking/`
- `(proposed) timesheetandexport/`
- `(proposed) desktopclient/`

## Prohibited Paths

- `08-commercial/**`
- `.git/**`

## Selected Technology

- **Technology**: C# on .NET 10 with the Avalonia UI desktop toolkit (rejected alternatives, do not use: WPF (Windows only, so it cannot run on the owner's Mac); .NET MAUI (no Linux support and weaker desktop support than Avalonia); WinForms (Windows only); A local web page or an Electron shell (not .NET, and a local port is a network surface the no-network promise forbids); Python with a Qt or Tkinter toolkit (rejected: the owner mandates .NET for all three examples)). Rationale: Application language and desktop UI toolkit. The owner mandates .NET. Avalonia UI gives a real native window, a system tray icon and a timer on Windows, macOS and Linux from one codebase, which matches the owner's Mac and the Windows target; the tray timer requires a tray icon. The app is published as a single-file, self-contained executable per platform (dotnet publish) and tested with xUnit.
- **Technology**: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (rejected alternatives, do not use: plain JSON or CSV files in a user folder (no transactions, so a crash mid-write corrupts the ledger)). Rationale: Database. SQLite is the mandated database. It is a single file with no server process, so the product keeps its local-first, no-server promise and a backup is a file copy.
- **Technology**: CSV export (rejected alternatives, do not use: PDF export). Rationale: The choice between CSV and PDF export depends on user needs for data presentation. CSV is favored for its simplicity, while PDF is preferred for formal documentation.

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

- `04e6e2e4e0b04159aa1067484e60d8aa` **Technology** (technology): C# on .NET 10 with the Avalonia UI desktop toolkit
- `25a2ec018af149ccaab74f8fbf8fbeda` **Technology** (technology): CSV export
- `8b91513dce6646c79aa70883f3c97f93` **Technology** (technology): an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite

## Evidence & Reporting Format

When a task is finished, record this report in the task's `checkpointUpdate` notes and in the pull request description:

- **Task**: the task key and title.
- **Status**: `completed`, or `blocked` with the reason.
- **Files changed**: every file added, changed or removed.
- **Commands run**: each command from the task's `commands`, with its result.
- **Tests**: the test that proves each item in the task's `tests` and `definitionOfDone`.
- **Locked decisions**: confirm none was changed (list ids if one was touched; that requires escalation first).
- **Deviations and escalations**: anything done differently from the packet, or escalated, and to whom.

