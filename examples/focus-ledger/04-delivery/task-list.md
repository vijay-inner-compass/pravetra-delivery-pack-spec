# Task List

| Primary tasks | Sub-tasks | Must requirements carried | Ready now | Waiting on a dependency | Blocked |
| --- | --- | --- | --- | --- | --- |
| 4 | 19 | 16 | TASK-001 | 22 | none |

Work from the top. A primary task is the skeleton of one component; its sub-tasks (indented) each deliver one unit of functionality after it. Each line: status, task, short title, component kind, what it waits for.

- [ ] **TASK-001** Scaffold Local Encrypted Database (DataStore) · depends on: (none)
  - [ ] **TASK-001.1** Store all session data · DataStore · depends on: TASK-001
  - [ ] **TASK-001.2** Encrypt all stored data at rest using AES-256 encryption · DataStore · depends on: TASK-001
  - [ ] **TASK-001.3** Provide a backup and recovery mechanism that allows users · DataStore · depends on: TASK-001
  - [ ] **TASK-001.4** Comply with GDPR regulations · DataStore · depends on: TASK-001
  - [ ] **TASK-001.5** Edit or delete past focus sessions · DataStore · depends on: TASK-001
- [ ] **TASK-002** Scaffold Session Tracking (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-002.1** Accurately track billable hours · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.2** Start a focus session by selecting a client and entering · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.3** Prompt the user · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.4** Timer updates in real-time · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.5** Start and record focus sessions · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.6** Manually stop a focus session and record the end time · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.7** Session data is backed up at least once a week to prevent · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.8** Access historical session data (+1 related Should requirement) · LogicalModule · depends on: TASK-002
- [ ] **TASK-003** Scaffold Timesheet and Export (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-003.1** Provide users with a trustworthy weekly timesheet · LogicalModule · depends on: TASK-003
  - [ ] **TASK-003.2** Export timesheet as a CSV or PDF file · LogicalModule · depends on: TASK-003
- [ ] **TASK-004** Scaffold Desktop Client (ClientApp) · depends on: TASK-001, TASK-002, TASK-003
  - [ ] **TASK-004.1** Display a timer in the system tray that counts the duration · ClientApp · depends on: TASK-004
  - [ ] **TASK-004.2** Provide a weekly review screen that totals sessions · ClientApp · depends on: TASK-004
  - [ ] **TASK-004.3** View a history of past focus sessions · ClientApp · depends on: TASK-004
  - [ ] **TASK-004.4** Have a user interface that adheres (+1 related Should requirement) · ClientApp · depends on: TASK-004

## Dependency Map

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
