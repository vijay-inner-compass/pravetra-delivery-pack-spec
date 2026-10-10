# Common Rules For Every Task

Each `TASK-nnn.md` in `04-delivery/` lists only what is specific to that task. The rules below are the same for every task of this pack, so they are written once, here. Read this file before the first task and follow it for every task. The `TASK-nnn.json` files still carry every line (the Markdown is the readable form of the same packet).

## How to work a task

1. Write the tests listed under "Write these tests first" and see them fail.
2. Implement the steps in order, inside the task's scope, without touching anything it lists as out of scope.
3. Run the commands the task lists; every test must pass and the build must be green.
4. Update the checkpoint (below), report which test proves each "Done when" item, then stop.

## Always prohibited

The task's own "Prohibited (this task)" list adds to these, it never removes one.

- Implementing feature or requirement behaviour: that belongs to the sub-tasks of this component.
- Modifying another task's target scope without an explicit, recorded dependency.
- Introducing an unapproved external package, dependency, or architecture style not recorded in the Solution Blueprint.
- Mutating applied database migrations in place - always create a new migration for schema changes.
- Committing hardcoded secrets, API keys, credentials, or environment-specific values.
- Altering or circumventing locked user decisions and governance constraints.
- Transmitting, caching, or routing sensitive or customer data to external regions or unapproved third-party endpoints.
- Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.
- Implementing a requirement that belongs to another sub-task of the same component, or to another component's task.

## Quality and security baseline

- Standard authentication and role-based authorization at every trust boundary this task touches.
- No secret or environment configuration hard-coded — route all credentials through the Secrets service.
- Clean architecture boundaries: adhere to separation of concerns and dependency inversion.

## Pack-wide policies and governance constraints

These come from the project's governance answers and apply to every task.

- Data residency & lifecycle policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat…
- Sensitive data governance & tokenization: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat…
- Human oversight & approval requirements: The head of platform engineering is the Technical Decision Owner and also the Risk Owner who tracks and mitigates the risks, the main one being score distrust. Evidence published for each gate review is the architecture diagram, the test coverage report and the replay-test results, and the head of platform engineering approves the pilot and the full rollout and holds the veto. Exceptions and accep…
- Security & encryption standard: Users sign in with the company single sign-on (OpenID Connect through ASP.NET Core authentication) and get team-scoped role-based access with least privilege, and each webhook source is authenticated with its own shared secret that is rotated quarterly and rejected otherwise. All traffic uses TLS 1.3, the database file sits on an encrypted disk volume, and secrets live in the server's protected co…
- Governance constraint (data residency): do not do the following - Transmitting, caching, or routing sensitive or customer data to external regions or unapproved third-party endpoints.
- Governance constraint (human approval): do not do the following - Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.

## Tests every task also needs

- Full regression test suite remains 100% green - this task must not regress another component.
- Negative scenario: Verify unauthorized request rejection across component trust boundaries.
- Boundary condition: Verify boundary thresholds, empty collections, and null state handling.

## Done for every task

- Every step in Implementation Steps is complete.
- Every item in Tests passes.
- The repository's standard build and test commands (see Commands) are green.
- No unresolved 'to be decided' marker remains anywhere this task touched.
- This task's checkpointUpdate has been applied to execution-state.json.

## Rollback

- git revert this task's commit(s) rather than editing history.
- If a database migration was applied, roll it back before reverting code — never edit an already-applied migration in place.

## Checkpoint

Set this task's status to 'completed' and record completedAt, then recompute nextSafeAction as the first remaining not_started task whose dependsOn are all completed.

Writes to: `07-agent/execution-state.json` - fields: tasks[].status, tasks[].completedAt, nextSafeAction

## Escalate to a human (stop, do not decide)

A task's own "Escalate if" list adds to these.

- Completing this task's Outcome would require an architecture, data-model, or public-contract choice not already recorded in the Solution Blueprint — stop and ask a human rather than deciding it yourself.
- A required credential, access grant, or environment value is missing.
- The repository's actual current state no longer matches this task's pinned baseline (see START_HERE.md's baseline-drift reconciliation guidance).
- A required human approval workflow or sign-off checkpoint is absent or bypassed.
- Data residency or geographic isolation boundaries would be violated.

