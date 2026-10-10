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
- Persisting unmasked PII, credentials, or sensitive data in server logs or unencrypted data stores.
- Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.
- Implementing a requirement that belongs to another sub-task of the same component, or to another component's task.

## Quality and security baseline

- Input validation at every file, clipboard and import boundary; encrypt data at rest as the data decision requires; no network trust boundary exists.
- No secret or key hard-coded or stored beside the data — keep encryption keys in the operating-system key store (or derive them from user input), never in source, the database file or logs.
- Clean architecture boundaries: adhere to separation of concerns and dependency inversion.

## Pack-wide policies and governance constraints

These come from the project's governance answers and apply to every task.

- Data residency & lifecycle policy: The data entities are client names, task descriptions, session start and end times and notes entered by the user; they are created by the user in the app, are available and clean from the first session, and are owned by the user, with the schema versioned inside the app by migration scripts. Data quality is validated on entry (a session needs a client and a start time, overlapping sessions are fla…
- Sensitive data governance & tokenization: The data entities are client names, task descriptions, session start and end times and notes entered by the user; they are created by the user in the app, are available and clean from the first session, and are owned by the user, with the schema versioned inside the app by migration scripts. Data quality is validated on entry (a session needs a client and a start time, overlapping sessions are fla…
- Human oversight & approval requirements: The product lead is the Technical Decision Owner and also the Risk Owner who tracks and mitigates risks, the main one being data loss with no cloud copy. Evidence published for each release review is the test coverage report, the backup restore test result and the signed-installer verification, and the product lead approves each release and holds the veto. Exceptions and accepted risks are recorde…
- Security & encryption standard: There are no accounts: the user is the owner of the machine and the operating system login is the only identity, and no other process is granted access to the database key held in the secure store. Data is encrypted at rest with AES-256, never leaves the machine (the update check carries no user data, and installers and updates are code-signed), and there are no secrets to manage on a server. Clie…
- Governance constraint (sensitive data): do not do the following - Persisting unmasked PII, credentials, or sensitive data in server logs or unencrypted data stores.
- Governance constraint (human approval): do not do the following - Bypassing human approval or oversight checkpoints for irreversible or high-impact actions.

## Tests every task also needs

- Full regression test suite remains 100% green - this task must not regress another component.
- Negative scenario: Verify a corrupt or tampered database file, a malformed import and a missing key are rejected with a clear message and no data loss.
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

