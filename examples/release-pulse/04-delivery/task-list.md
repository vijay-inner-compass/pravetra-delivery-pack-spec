# Task List

| Primary tasks | Sub-tasks | Must requirements carried | Ready now | Waiting on a dependency | Blocked |
| --- | --- | --- | --- | --- | --- |
| 8 | 21 | 15 | TASK-001 | 28 | none |

Work from the top. A primary task is the skeleton of one component; its sub-tasks (indented) each deliver one unit of functionality after it. Each line: status, task, short title, component kind, what it waits for.

- [ ] **TASK-001** Scaffold Primary Database (DataStore) · depends on: (none)
  - [ ] **TASK-001.1** Ensure the application complies · DataStore · depends on: TASK-001
- [ ] **TASK-002** Scaffold API / Backend Service (DeployableUnit) · depends on: TASK-001
  - [ ] **TASK-002.1** Surface repeated risky release patterns · DeployableUnit · depends on: TASK-002
  - [ ] **TASK-002.2** Integrate with the CI system to receive deploy · DeployableUnit · depends on: TASK-002
  - [ ] **TASK-002.3** Integrate with the incident tracking tool to receive · DeployableUnit · depends on: TASK-002
  - [ ] **TASK-002.4** Implement data encryption in transit and at rest · DeployableUnit · depends on: TASK-002
  - [ ] **TASK-002.5** Implement role-based access control for engineering managers · DeployableUnit · depends on: TASK-002
  - [ ] **TASK-002.6** Ensure the application is scalable (+1 related Should requirement) · DeployableUnit · depends on: TASK-002
- [ ] **TASK-003** Scaffold Data Quality (LogicalModule) · depends on: TASK-001, TASK-002
  - [ ] **TASK-003.1** Maintain an audit log of all actions taken · LogicalModule · depends on: TASK-003
- [ ] **TASK-004** Scaffold Release Health Analytics (LogicalModule) · depends on: TASK-001, TASK-002
  - [ ] **TASK-004.1** Normalize incoming deploy and incident data to ensure · LogicalModule · depends on: TASK-004
  - [ ] **TASK-004.2** Calculate a release-health score · LogicalModule · depends on: TASK-004
  - [ ] **TASK-004.3** Application provides insights into the release health · LogicalModule · depends on: TASK-004
  - [ ] **TASK-004.4** Compare release health scores across different teams · LogicalModule · depends on: TASK-004
- [ ] **TASK-005** Scaffold Digest Worker (BackgroundWorker) · depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - [ ] **TASK-005.1** Compile a summary of release health · BackgroundWorker · depends on: TASK-005
  - [ ] **TASK-005.2** Ensure the application is available during working hours · BackgroundWorker · depends on: TASK-005
  - [ ] **TASK-005.3** Provide notifications to on-call engineers · BackgroundWorker · depends on: TASK-005
- [ ] **TASK-006** Scaffold Ingest Worker (BackgroundWorker) · depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - [ ] **TASK-006.1** Process incoming webhook events · BackgroundWorker · depends on: TASK-006
- [ ] **TASK-007** Scaffold Scoring Worker (BackgroundWorker) · depends on: TASK-001, TASK-002, TASK-003, TASK-004
  - [ ] **TASK-007.1** Run the scoring worker as own background process · BackgroundWorker · depends on: TASK-007
  - [ ] **TASK-007.2** Take work · BackgroundWorker · depends on: TASK-007
  - [ ] **TASK-007.3** Retry failed items · BackgroundWorker · depends on: TASK-007
- [ ] **TASK-008** Scaffold Web Client (ClientApp) · depends on: TASK-001, TASK-002, TASK-003, TASK-004, TASK-005, TASK-006, TASK-007
  - [ ] **TASK-008.1** Provide a consistent · ClientApp · depends on: TASK-008
  - [ ] **TASK-008.2** Provide a user interface that allows engineering managers · ClientApp · depends on: TASK-008

## Dependency Map

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
