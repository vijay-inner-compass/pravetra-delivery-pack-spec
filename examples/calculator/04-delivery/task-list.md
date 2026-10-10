# Task List

| Primary tasks | Sub-tasks | Must requirements carried | Ready now | Waiting on a dependency | Blocked |
| --- | --- | --- | --- | --- | --- |
| 6 | 20 | 16 | TASK-001 | 25 | none |

Work from the top. A primary task is the skeleton of one component; its sub-tasks (indented) each deliver one unit of functionality after it. Each line: status, task, short title, component kind, what it waits for.

- [ ] **TASK-001** Scaffold Local Data Store (DataStore) · depends on: (none)
  - [ ] **TASK-001.1** Maintain a local SQLite database to store the last 10 · DataStore · depends on: TASK-001
  - [ ] **TASK-001.2** Ensure data retention by maintaining the last 10 · DataStore · depends on: TASK-001
- [ ] **TASK-002** Scaffold Calculation History (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-002.1** Provide audit logging (+1 related Should requirement) · LogicalModule · depends on: TASK-002
  - [ ] **TASK-002.2** Delete calculation history from the SQLite database · LogicalModule · depends on: TASK-002
- [ ] **TASK-003** Scaffold Error Reporting (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-003.1** Provide clear error messages for malformed expressions · LogicalModule · depends on: TASK-003
  - [ ] **TASK-003.2** Accurately evaluate division operations · LogicalModule · depends on: TASK-003
- [ ] **TASK-004** Scaffold Expression Evaluation (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-004.1** Evaluate arithmetic expressions · LogicalModule · depends on: TASK-004
  - [ ] **TASK-004.2** Evaluate arithmetic expressions quickly enough · LogicalModule · depends on: TASK-004
- [ ] **TASK-005** Scaffold Rounding and Precision (LogicalModule) · depends on: TASK-001
  - [ ] **TASK-005.1** Handle rounding using decimal arithmetic to avoid · LogicalModule · depends on: TASK-005
  - [ ] **TASK-005.2** Use decimal arithmetic for all calculations to ensure · LogicalModule · depends on: TASK-005
  - [ ] **TASK-005.3** All arithmetic operations are performed · LogicalModule · depends on: TASK-005
- [ ] **TASK-006** Scaffold Console Host (DeployableUnit) · depends on: TASK-001, TASK-002, TASK-003, TASK-004, TASK-005
  - [ ] **TASK-006.1** Reduce the error rate in invoice total calculations · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.2** Minimize rework time associated · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.3** Run locally on each analyst's laptop · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.4** Available to analysts whenever they work · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.5** Input arithmetic expressions directly into the terminal · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.6** Ensure the command-line calculator is compatible · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.7** Ensure compliance with internal data handling policies · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.8** Ensure the command-line calculator provides accurate results · DeployableUnit · depends on: TASK-006
  - [ ] **TASK-006.9** Provide built-in help documentation (+2 related Should requirements) · DeployableUnit · depends on: TASK-006

## Dependency Map

| Task | Depends On | Unlocks |
| --- | --- | --- |
| TASK-001 | (none) | TASK-001.1, TASK-001.2, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006 |
| TASK-001.1 | TASK-001 | (none) |
| TASK-001.2 | TASK-001 | (none) |
| TASK-002 | TASK-001 | TASK-002.1, TASK-002.2, TASK-006 |
| TASK-002.1 | TASK-002 | (none) |
| TASK-002.2 | TASK-002 | (none) |
| TASK-003 | TASK-001 | TASK-003.1, TASK-003.2, TASK-006 |
| TASK-003.1 | TASK-003 | (none) |
| TASK-003.2 | TASK-003 | (none) |
| TASK-004 | TASK-001 | TASK-004.1, TASK-004.2, TASK-006 |
| TASK-004.1 | TASK-004 | (none) |
| TASK-004.2 | TASK-004 | (none) |
| TASK-005 | TASK-001 | TASK-005.1, TASK-005.2, TASK-005.3, TASK-006 |
| TASK-005.1 | TASK-005 | (none) |
| TASK-005.2 | TASK-005 | (none) |
| TASK-005.3 | TASK-005 | (none) |
| TASK-006 | TASK-001, TASK-002, TASK-003, TASK-004, TASK-005 | TASK-006.1, TASK-006.2, TASK-006.3, TASK-006.4, TASK-006.5, TASK-006.6, TASK-006.7, TASK-006.8, TASK-006.9 |
| TASK-006.1 | TASK-006 | (none) |
| TASK-006.2 | TASK-006 | (none) |
| TASK-006.3 | TASK-006 | (none) |
| TASK-006.4 | TASK-006 | (none) |
| TASK-006.5 | TASK-006 | (none) |
| TASK-006.6 | TASK-006 | (none) |
| TASK-006.7 | TASK-006 | (none) |
| TASK-006.8 | TASK-006 | (none) |
| TASK-006.9 | TASK-006 | (none) |
