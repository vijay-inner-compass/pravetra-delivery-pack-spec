# TASK-001.1 — Store all session data

- **Component:** Local Encrypted Database · sub-task of TASK-001 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
> **Requirement:** The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.

## Done when
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Must] The application must store all session data, including cl...: Given valid input, when the function described by this requirement is used, then the system does what it states: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
- Also: Acceptance (negative) for [Must] The application must store all session data, including cl...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Out of scope
- the other sub-tasks of this component - TASK-001.2 (Encrypt all stored data at rest using AES-256 encryption); TASK-001.3 (Provide a backup and recovery mechanism that allows users); TASK-001.4 (Comply with GDPR regulations); TASK-001.5 (Edit or delete past focus sessions).
- the responsibilities of the other components - Session Tracking, Timesheet and Export, Desktop Client.

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
| `(proposed) localencrypteddatabase/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (localencrypteddatabase/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Local Encrypted Database'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-001 builds and its health check passes.
2. Implement: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Embedded relational schema with versioned local upgrades; the file is created on first run and never leaves the user's machine unless the user exports it.
6. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
Accessed only through the domain modules, in-process, through the embedded database driver; no network access.

## Quality and Security (this task)
- Data handling and retention specification: Embedded relational schema with versioned local upgrades; the file is created on first run and never leaves the user's machine unless the user exports it.
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.
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
Builds on the skeleton of 'Local Encrypted Database' delivered by TASK-001. Greenfield component per Solution Blueprint. Target responsibilities:
• Persist the application's data in a single local database file on the user's machine.
• Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store).
• Support backup and restore of the one file, and versioned local schema upgrades when the application is updated.
- **Source references:** BlueprintComponent: Local Encrypted Database (`386f3f2fb8fc44b7ad3c90e6f2d89ddb`); Requirement: [Must] Store all session data (`d9527b35c4494cb2807211133ea4b2f0`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
