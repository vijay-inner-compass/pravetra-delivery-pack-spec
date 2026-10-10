# TASK-002.2 — Start a focus session by selecting a client and entering

- **Component:** Session Tracking · sub-task of TASK-002 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-002 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Start a focus session by selecting a client and entering a one-line task description.
> **Requirement:** The application must allow users to start a focus session by selecting a client and entering a one-line task description.

## Done when
- [ ] Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- [ ] Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to start a focus session by selecting a client and entering a one-line task description.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- negative case: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- positive case: Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to start a focus session by selecting a client and entering a one-line task description.
- Also: Acceptance (negative) for [Must] The application must allow users to start a focus session...: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.
- Also: Acceptance (positive) for [Must] The application must allow users to start a focus session...: Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to start a focus session by selecting a client and entering a one-line task description.

## Out of scope
- the other sub-tasks of this component - TASK-002.1 (Accurately track billable hours); TASK-002.3 (Prompt the user); TASK-002.4 (Timer updates in real-time); TASK-002.5 (Start and record focus sessions); TASK-002.6 (Manually stop a focus session and record the end time); TASK-002.7 (Session data is backed up at least once a week to prevent); TASK-002.8 (Access historical session data (+1 related Should require...).
- the responsibilities of the other components - Local Encrypted Database, Timesheet and Export, Desktop Client.

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
| `(proposed) sessiontracking/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (sessiontracking/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Session Tracking'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-002 builds and its health check passes.
2. Implement: The application must allow users to start a focus session by selecting a client and entering a one-line task description.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
6. Implement the failure behaviour the negative acceptance criteria describe: Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

## Contract
In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.

## Quality and Security (this task)
- Data handling and retention specification: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- Architecture decomposition boundary: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.
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
Builds on the skeleton of 'Session Tracking' delivered by TASK-002. Greenfield component per Solution Blueprint. Target responsibilities:
• Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Source references:** BlueprintComponent: Session Tracking (`10abc4b7178f40a8aa5248ba6e52061d`); Requirement: [Must] Start a focus session by selecting a client and entering a one-line task (`9fd91fb5542344b7b96640c91c3183f7`); TechnologyDecision: Technology: C# on .NET 10 with the Avalonia UI desktop toolkit (`04e6e2e4e0b04159aa1067484e60d8aa`); TechnologyDecision: Technology: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (`8b91513dce6646c79aa70883f3c97f93`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
