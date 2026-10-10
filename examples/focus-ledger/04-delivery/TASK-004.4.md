# TASK-004.4 — Have a user interface that adheres (+1 related Should requirement)

- **Component:** Desktop Client · sub-task of TASK-004 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-004 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Have a user interface that adheres to accessibility standards, ensuring usability for all users.
> **Requirement:** The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
> **Requirement:** The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

## Done when
- [ ] Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
- [ ] Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
- positive case: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.
- negative case: invalid, unauthorised or malformed input for this behaviour is rejected with a clear error.
- Also: Acceptance (positive) for [Should] The application must have a user interface that adheres t...: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
- Also: Acceptance (positive) for [Should] The application must ensure that the user interface is re...: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

## Out of scope
- the other sub-tasks of this component - TASK-004.1 (Display a timer in the system tray that counts the duration); TASK-004.2 (Provide a weekly review screen that totals sessions); TASK-004.3 (View a history of past focus sessions).
- the responsibilities of the other components - Local Encrypted Database, Session Tracking, Timesheet and Export.

## Applicable decisions
- [04e6e2e4e0b04159aa1067484e60d8aa] Technology: C# on .NET 10 with the Avalonia UI desktop toolkit
- [8b91513dce6646c79aa70883f3c97f93] Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite
- [25a2ec018af149ccaab74f8fbf8fbeda] Technology: CSV export
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (2 listed), each shown by a named test or check.
- [ ] Every test under "Write these tests first" exists, failed before the change, and passes now.
- [ ] The applicable decisions and the common rules are respected and nothing contradicts them.
- [ ] The out-of-scope items are untouched.
- [ ] No unrelated changes: the diff stays inside the allowed paths and only this sub-task's behaviour changed.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET 10 with the Avalonia UI desktop toolkit).
- Do not substitute, replace, or alter the locked decision for Technology (an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite).
- Do not substitute, replace, or alter the locked decision for Technology (CSV export).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) desktopclient/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (desktopclient/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Desktop Client'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-004 builds and its health check passes.
2. Implement: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
3. Implement: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.
4. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
5. Align the component interface with its contract: (see Contract)
6. Keep to the component's data design: Holds transient interface state only; all durable data is read and written through the local data store.

## Contract
No network API. The client calls the domain modules in-process; import and export file formats, if any, are recorded here.

## Quality and Security (this task)
- Data handling and retention specification: Holds transient interface state only; all durable data is read and written through the local data store.
- Architecture decomposition boundary: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.
- Non-functional target (The application must ensure that the timer updates in rea...): The application must ensure that the timer updates in real-time with a maximum latency of 1 second.
- Non-functional target (The application must start and record focus sessions with...): The application must start and record focus sessions without a network connection, so the timer is available whenever the user's computer is on.
- Non-functional target (The application must encrypt all stored data at rest usin...): The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information.
- Non-functional target (The application must allow users to access their historic...): The application must allow users to access their historical session data for as long as they keep it.
- Non-functional target (The application must provide a backup and recovery mechan...): The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file.
- Non-functional target (The application must comply with GDPR regulations, allowi...): The application must comply with GDPR regulations, allowing users to delete their data upon request.
- Non-functional target (The application must have a user interface that adheres t...): The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.
- Non-functional target (The application must ensure that the user interface is re...): The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.
- Non-functional target (The application must ensure that session data is backed u...): The application must ensure that session data is backed up at least once a week to prevent data loss.

## Current State Evidence
Builds on the skeleton of 'Desktop Client' delivered by TASK-004. Greenfield component per Solution Blueprint. Target responsibilities:
• Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems.
• Run the domain modules in-process on the user's machine; no network service is involved.
• Keep window and view state locally; every durable fact goes through the local data store.
- **Source references:** BlueprintComponent: Desktop Client (`9a730da684404e80880bd8ddcf6b6db8`); Requirement: [Should] Have a user interface that adheres to accessibility standards (`e1d429643cc7408d9c005d08f4386f2f`); Requirement: [Should] User interface is responsive (`e1a2605dde7242deb5b8a06e426b7ad7`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
