# Pravetra Universal Delivery Pack Specification (v1.1)
**Standardized Architecture & Task Handoff Protocol for Autonomous Coding Agents**

**Status**: Draft v1.1  
**License**: Apache-2.0 (see [LICENSE](LICENSE))  
**Specification Suite**:
- [Conformance Guide](CONFORMANCE.md)
- [Extension Guide](EXTENSIONS.md)
- [Changelog](CHANGELOG.md)
- [JSON Schemas v1](schemas/v1/)
- [Test Vectors](test-vectors/)

---

## 1. Overview & Purpose
The **Universal Delivery Pack** is an open, vendor-neutral specification for packaging verified software architectures, governance constraints, domain data models, and dependency-ordered atomic task packets for consumption by autonomous coding agents (Claude Code, Gemini CLI, Cursor, Copilot Workspace, Devin, and specialized orchestrators like `pravetra-conductor`).

Rather than passing raw, unconstrained chat prompts to AI models, a Delivery Pack provides a deterministic, version-pinned, tamper-evident contract between software architects and autonomous execution engines.

Tagline: *"Intelligence from idea to outcome."*

---

## 2. Directory Layout Standard

Every valid Delivery Pack archive (`.zip`) or expanded workspace folder contains the following 8 numbered sections:

```
<delivery-pack-root>/
├── 00-manifest/
│   ├── MANIFEST.md                       # Pack metadata, timestamp, target agents
│   ├── manifest.json                     # Canonical machine-readable protocol envelope
│   ├── executive-dossier.md              # Executive summary & decision governance
│   ├── executive-dossier.pdf             # Formatted dossier
│   └── executive-dossier.html            # Visual interactive viewer
├── 01-baseline/
│   └── baseline-pin.md                   # Pinned repository commit, branch, or greenfield baseline
├── 02-context/
│   ├── context-summary.md                # System context, scope boundaries, integrations
│   ├── requirements.md                   # Full requirements breakdown (Agile/Scrum/SAFe/SDLC)
│   └── requirements.html                 # Interactive requirements viewer
├── 03-architecture/
│   ├── architecture-summary.md           # High-Level Architecture (HLD), ADRs, topology
│   ├── architecture-summary.html         # Visual diagrams and interactive models
│   ├── domain-data-model.md              # Domain entities, aggregate roots, persistence rules
│   └── domain-data-model.html            # Schema and relationship viewer
├── 04-delivery/
│   ├── task-list.md                      # Dependency-ordered task list and milestone map
│   ├── implementation-readiness-report.md# Gate 4 readiness checks, quality gates, blockers
│   ├── TASK-001.json                     # Canonical JSON task packet (machine-readable)
│   ├── TASK-001.md                       # Rendered Markdown task packet (human-readable; layout non-normative)
│   └── TASK-NNN...                       # Subsequent atomic task packets
├── 05-quality/
│   └── quality-and-security.md           # Quality standards, security thresholds, testing matrix
├── 06-ops/
│   └── deployment-and-rollback.md        # Environment specs, deployment scripts, rollback steps
└── 07-agent/
    ├── START_HERE.md                     # [Normative] Agent onboarding, mission briefing and operating rules
    ├── START_HERE.pdf                    # Visual briefing
    ├── execution-state.json              # [Normative] Checkpoint tracker & state machine
    ├── COMMON_RULES.md                   # [Non-Normative, optional] Rules every task shares (written once, not per task)
    ├── implementation-prompt.md          # Optional ready-to-paste prompt (and .pdf)
    ├── coding-agent-instructions-guide.md# Optional guide to the policy files (and .pdf)
    ├── AGENTS.md                         # [Non-Normative] Agent policy in the AGENTS.md convention
    ├── CLAUDE.md, GEMINI.md, AGENT_POLICY.md, CONVENTIONS.md, replit.md, .clinerules
    ├── .claude/skills/*.md               # [Non-Normative] Vendor policy files, each at the path its tool reads
    ├── .github/copilot-instructions.md   #   (.cursor/rules/, .continue/rules/, .roo/rules/, .kilo/rules/, .kiro/steering/,
    └── .agents/, .devin/, .warp/, .junie/, .factory/, .config/{zed,amp,opencode}/ ...  likewise)
```

### 2.1 Section contents

| Section | Contents | Required by |
|---|---|---|
| `00-manifest/` | `manifest.json` (the protocol envelope, section 3) and `MANIFEST.md` (the same facts for people). Executive dossier files are optional (`DeliveryPack.Full`). | all profiles |
| `01-baseline/` | `baseline-pin.md`: the repository commit, branch or greenfield marker the tasks were written against. | all profiles |
| `02-context/` | `context-summary.md` and `requirements.md` (plus optional gate summaries and HTML viewers). | all profiles |
| `03-architecture/` | `architecture-summary.md` (plus optional diagrams, `domain-data-model.md`, and HTML viewers). | all profiles |
| `04-delivery/` | `task-list.md` and, for each task, `TASK-NNN.json` (normative, section 5) and `TASK-NNN.md` (the same content for people; its layout is **non-normative**, see below). Optional: `implementation-readiness-report.md`. | `Execution` and above |
| `05-quality/` | `quality-and-security.md`. | `Governance` and above |
| `06-ops/` | `deployment-and-rollback.md`. | `Governance` and above |
| `07-agent/` | `START_HERE.md` and `execution-state.json` (normative, section 6) plus vendor policy files (non-normative, section 7). | `Execution` and above |
| `08-commercial/` | Optional; never read or changed by an agent (see the note below). Not listed in the manifest and not covered by `integrity.hash`. | none |

**The Markdown files are not normative.** `TASK-NNN.md`, `task-list.md` and `MANIFEST.md` are written for people; a consumer reads the JSON files (and `manifest.json`), never the headings or wording of the Markdown. A generator is free to lay the Markdown out as it finds most readable. Pravetra's current layout puts a summary first (component, depends on / unlocks, outcome, done-when, tests to write first, out of scope, applicable decisions, reviewer checklist), then the scope tables, steps and evidence, and moves the lines that are the same in every task (the always-prohibited list, quality baseline, standard done items, rollback, standard escalation conditions) into one optional file, `07-agent/COMMON_RULES.md`, which each task file points to. The JSON packet always carries every line, so a consumer that reads only JSON loses nothing. A sub-task's `title` may be a short verb phrase derived from its requirement; `title` is free text. The `examples/` packs use the earlier Markdown layout, which remains valid.

### 2.2 The 07-agent root layout

Vendor policy files are written **directly under `07-agent/`, each at the relative path its tool expects** (`07-agent/AGENTS.md`,
`07-agent/GEMINI.md`, `07-agent/.cursor/rules/...`). Copying the contents of `07-agent/` into a repository root therefore installs the
policy for every selected tool, with no renaming. They are non-normative: a consumer relies only on `START_HERE.md`, `execution-state.json`
and the task packets, and MUST ignore policy files it does not recognise. An earlier draft placed these under `07-agent/extensions/<vendor>/`;
that location is no longer used, and `execution-policy.json`, `capabilities.json` and `instructions.md` are not part of the Execution profile
(the same rules are stated in `START_HERE.md` and in each task packet's `allowedChanges`, `prohibitedChanges` and `securityConstraints`).

> **Note on Commercial Data (08-commercial/)**: If attached by commercial governance modules, financial models, pricing tiers, and licensing agreements reside in `08-commercial/`. Autonomous coding agents are strictly prohibited from reading, modifying, or disclosing files in `08-commercial/`.

---

## 3. Protocol Manifest Envelope (`00-manifest/manifest.json`)

The manifest protocol envelope defines the top-level identity, conformance level, generator provenance, and integrity hash of the delivery pack. It validates against [`delivery-pack-manifest.schema.json`](schemas/v1/delivery-pack-manifest.schema.json). The example below is the manifest of the published test vector `test-vectors/dp-2026-001/`:

```json
{
  "specVersion": "1.0.0",
  "packId": "DP-2026-001",
  "createdAt": "2026-10-06T18:00:00Z",
  "generator": {
    "name": "ExampleGenerator",
    "version": "1.0.0",
    "url": "https://example.com/example-generator"
  },
  "conformanceLevel": "DeliveryPack.Execution",
  "integrity": {
    "algorithm": "sha256",
    "hash": "a54634a933b0f19931f447d7cb8748fc88d15bb294e0c748bb6849e5b31179f0"
  },
  "capabilities": [
    "worktree-isolation"
  ],
  "policies": [
    "strict-scope-confinement",
    "no-bypass-gates"
  ],
  "tasks": [
    "TASK-001",
    "TASK-002"
  ],
  "sections": [
    {
      "section": "00-manifest",
      "files": [
        "MANIFEST.md",
        "manifest.json"
      ]
    },
    {
      "section": "01-baseline",
      "files": [
        "baseline-pin.md"
      ]
    },
    {
      "section": "02-context",
      "files": [
        "context-summary.md",
        "requirements.md"
      ]
    },
    {
      "section": "03-architecture",
      "files": [
        "architecture-summary.md"
      ]
    },
    {
      "section": "04-delivery",
      "files": [
        "TASK-001.json",
        "TASK-001.md",
        "TASK-002.json",
        "TASK-002.md",
        "task-list.md"
      ]
    },
    {
      "section": "07-agent",
      "files": [
        "AGENTS.md",
        "START_HERE.md",
        "execution-state.json"
      ]
    }
  ]
}
```

| Field | Rule |
|---|---|
| `specVersion` | The specification version the pack conforms to (`1.x.y`). |
| `packId` | Unique id chosen by the generator: letters, digits, `.`, `_`, `-`; 3 to 128 characters. Pravetra writes `pravetra-<project id>-v<pack version>`. |
| `generator` | `name` and `version` of the tool that produced the pack. |
| `conformanceLevel` | The one profile the pack claims (section 4). A generator claims only what it can prove: Pravetra claims `DeliveryPack.Execution`, or `DeliveryPack.Core` for a pack with no task packet. |
| `tasks` | The task ids, in dependency order (a task appears after every task it depends on). |
| `sections` | Every file of the pack that the manifest vouches for, as `{section, files[]}` with file paths relative to the section folder. Includes `manifest.json` itself. |
| `integrity` | `algorithm` (`sha256` or `sha512`) and `hash` (lowercase hex; 64 characters for sha256, 128 for sha512). Computed as defined in 3.1. |
| `capabilities`, `policies`, `artifacts` | Optional lists of strings; a generator that does not know what to put there writes an empty `capabilities` array rather than guess. |

### 3.1 What `integrity.hash` covers

The hash is computed over a **defined file list**, so any two implementations produce the same value:

1. **Covered files**: every file listed in the manifest's `sections` (as `<section>/<file>`) **except `00-manifest/manifest.json` itself** (a file cannot contain its own hash). Files that exist in the pack but are not listed (for example `CHECKSUMS.sha256`, or anything in `08-commercial/`) are not covered.
2. **Per-file digest**: the digest, in the manifest's `algorithm`, of the file's exact bytes as stored in the pack, written as lowercase hex.
3. **Checksum text**: one line per covered file, `<digest>`, two spaces, `<path relative to the pack root, with "/" separators>`, then a line feed (`\n`, never CRLF). The lines are ordered by the UTF-8 bytes of the path, ascending (plain byte-wise ordering, not locale-aware). This is the format `sha256sum` writes, so on a Unix shell the covered files give the text with `sha256sum` over the sorted list.
4. **`integrity.hash`**: the digest, in the same `algorithm`, of the checksum text encoded as UTF-8 (no byte-order mark).

A consumer recomputes the value and rejects the pack when it differs, or when a listed file is missing. Anyone who changes a covered file after generation (for example regenerating one task packet) MUST recompute `integrity.hash` and rewrite `manifest.json`.

---

## 4. Conformance Levels

To support a wide spectrum of tools from simple documentation generators to full-lifecycle enterprise orchestrators, the specification defines 4 hierarchical conformance profiles (detailed in [CONFORMANCE.md](CONFORMANCE.md)):

1. **Delivery Pack Core (`DeliveryPack.Core`)**:
   - Minimum architectural handoff: Manifest, Baseline Pin (`01-baseline/`), System Context & Requirements (`02-context/`), and Architecture Summary (`03-architecture/`).
2. **Delivery Pack Execution (`DeliveryPack.Execution`)**:
   - Conforms to Core + Atomic Task Packets (`TASK-NNN.json`), Execution State Machine (`execution-state.json`), and the agent briefing (`07-agent/START_HERE.md`).
3. **Delivery Pack Governance (`DeliveryPack.Governance`)**:
   - Conforms to Execution + Quality Matrix (`05-quality/`), Deployment & Rollback Runbooks (`06-ops/`), Implementation Readiness Report, and SHA-256 cryptographic integrity verification.
4. **Delivery Pack Full (`DeliveryPack.Full`)**:
   - Conforms to Governance + Domain Data Models (`domain-data-model.md`), interactive visual HTML viewers, and isolated commercial boundary protection (`08-commercial/`).

---

## 5. Atomic Task Packet Contract (`TASK-NNN.json`)

Each task packet in `04-delivery/` represents a single, self-contained atomic unit of work with explicit pre-conditions, target paths, allowed changes, prohibited operations, automated test commands, and definition of done.

### Schema Fields
| Field | Type | Description |
|---|---|---|
| `taskId` | `string` | Unique task identifier (e.g. `TASK-001`, `TASK-002`), or `TASK-NNN.N` for a sub-task (e.g. `TASK-001.2`, section 5.1). |
| `parentTaskId` | `string \| null` | **Optional (1.1.0).** The task this one is a sub-task of; absent or null for a primary task (section 5.1). |
| `title` | `string` | Concise imperative description of the task objective. |
| `outcome` | `string` | Target deliverable produced upon task completion. |
| `status` | `string` | Current lifecycle status: `NotStarted`, `InProgress`, `Completed`, `Blocked`, `Cancelled`. |
| `sequence` | `integer` | Execution sequence number. |
| `parallelSafe` | `boolean` | True if this task can execute concurrently with others at the same dependency tier. |
| `humanApprovalRequired` | `boolean` | **Required.** True if human sign-off is required before merging changes; a consumer MUST stop for approval when it is true. Pravetra writes `true` on every task. |
| `dependsOn` | `string[]` | Prerequisite task IDs (each `TASK-NNN` or `TASK-NNN.N`, no duplicates) that must complete before this task begins. |
| `unlocks` | `string[]` | Downstream task IDs (each `TASK-NNN` or `TASK-NNN.N`, no duplicates) enabled upon this task's completion. |
| `targetScope` | `object[]` | List of explicit filesystem paths targeted by this task (`path`, `status`, `note`). |
| `inputs` | `string[]` | Input specifications, schemas, or contract files consulted during execution. |
| `expectedOutputs` | `string[]` | Deliverables produced upon completion. |
| `allowedCapabilities` | `string[]` | Permissions granted (e.g. `filesystem:read`, `filesystem:write`, `process:run`). |
| `allowedChanges` | `string[]` | Explicit authorized actions permitted during implementation. |
| `prohibitedChanges` | `string[]` | Explicit boundaries and forbidden actions (e.g., no modifying auth contracts). |
| `changeContract` | `string` | Summary of interface, schema, or functional contracts modified. |
| `implementationSteps` | `string[]` | Step-by-step guidance for the coding agent. |
| `qualityAndSecurity` | `string[]` | Security, data classification, and quality requirements. |
| `securityConstraints` | `string[]` | Specific runtime isolation or credential rules. |
| `tests` | `string[]` | Test assertions and acceptance criteria. |
| `commands` | `object[]` | Commands to run for compiling, testing, and verifying the work, each `{executable, args[], purpose, workingDirectory?}`. `executable` is one word (no spaces or shell metacharacters) started directly with `args`; never a shell string. May be empty when the build and test commands are not known (the packet then escalates). |
| `rollback` | `string[]` | Instructions to reverse changes if verification fails. |
| `artifactHashes` | `object` | Map of pack-relative artifact paths to expected SHA-256 hashes (64 hex characters). |
| `definitionOfDone` | `string[]` | Objective checklist required before marking the task complete. |
| `reviewerChecklist` | `string[]` | **Optional (1.1.0).** On a sub-task: the checklist a reviewer ticks off (criteria met, tests present and passing, decisions respected, out-of-scope untouched, no unrelated changes). |
| `escalateIf` | `string[]` | Conditions that require the agent to stop and request human assistance. |

### 5.1 Primary tasks and sub-tasks (1.1.0, optional)

A generator MAY split the work of a component into two levels: a **primary task** (`TASK-001`: the skeleton, wiring and a health check, nothing else) and **sub-tasks** (`TASK-001.1`, `TASK-001.2`, ...: one unit of working functionality each, with its own acceptance criteria, tests, allowed and prohibited paths and a "Done when" statement). A sub-task carries `parentTaskId` set to its primary task.

- The task id of a sub-task is `TASK-NNN.N`; its file is `04-delivery/TASK-NNN.N.json` (and `.md`).
- `parentTaskId` is optional and absent on a primary task. When present it MUST name a task in the pack, the chain of parents MUST NOT loop, and the sub-task MUST list its parent in `dependsOn`.
- The same optional `parentTaskId` appears on each entry of `execution-state.json` `tasks`; each sub-task is tracked and completed like any other task.
- A sub-task is written to be reviewed: its `definitionOfDone` starts with one `Done when: ...` line per acceptance criterion, its `tests` list the tests to write first (`Write first ...`, negative cases included), its `prohibitedChanges` carry `Out of scope ...` lines, and its `qualityAndSecurity` names the applicable decisions and a `Must not contradict` line. These are conventions of the existing string arrays, not new required fields.
- Each entry of `sourceRefs` names what a task was derived from. `entityType` is a free string (no enumeration in the schema); the Pravetra generator writes `Requirement`, `AcceptanceCriterion`, `BlueprintComponent`, `Decision`, `TechnologyDecision` and, since VR-286, `ComponentResponsibility`. A sub-task whose only source besides its component is a `ComponentResponsibility` reference (`entityId` is the component id, `#`, and the position of the responsibility) was built from a responsibility recorded for a component that no requirement reaches; it is flagged "Responsibility-derived" in its steps and quality lines and carries no `Requirement` reference. Consumers MUST ignore an `entityType` they do not know (VERSIONING.md section 4.1).
- `task-list.md` shows the hierarchy as an indented list. Ordering is unchanged: `sequence` and `dependsOn` decide the order, so a consumer that ignores `parentTaskId` still runs the pack correctly.
- A pack that does not use sub-tasks is unchanged and MAY keep declaring `specVersion` `1.0.0`; a pack that uses them declares `1.1.0` or later.

---

## 6. Execution State Machine (`execution-state.json`)

Located in `07-agent/execution-state.json`, this file maintains the authoritative runtime progress of the delivery pack across agent sessions. Generator-specific data (here, Pravetra's solution-blueprint identifiers) goes in the `extensions` object, keyed by vendor; consumers ignore keys they do not know:

```json
{
  "specVersion": "1.0.0",
  "deliveryPackVersion": 1,
  "pinnedRepositoryLabel": "main@d8203c53",
  "extensions": { "pravetra": { "blueprintId": "bp_4a89f012", "blueprintVersion": 1 } },
  "tasks": [
    {
      "taskId": "TASK-001",
      "title": "Primary Database & Persistence Setup",
      "status": "Completed",
      "dependsOn": [],
      "startedAt": "2026-10-06T18:05:00Z",
      "completedAt": "2026-10-06T18:12:30Z",
      "sourceCommit": "d8203c53",
      "executionAgent": "pravetra-conductor/1.0.0",
      "worktreePath": ".worktrees/TASK-001",
      "exitCode": 0
    },
    {
      "taskId": "TASK-002",
      "title": "Domain Entity Models & Migrations",
      "status": "InProgress",
      "dependsOn": ["TASK-001"],
      "startedAt": "2026-10-06T18:13:00Z",
      "completedAt": null,
      "executionAgent": "pravetra-conductor/1.0.0",
      "worktreePath": ".worktrees/TASK-002",
      "exitCode": null
    }
  ],
  "nextSafeAction": "Start TASK-002: Domain Entity Models & Migrations",
  "reconciliationGuidance": "If the repository's actual HEAD no longer matches the pinned baseline, stop and confirm before proceeding."
}
```

A task entry may also carry `sourceCommit` (optional, a 7 to 64 digit hexadecimal commit id): the repository commit that holds the task's work. `completedAt` and `sourceCommit` are written only for a completed task and are omitted otherwise.

---

## 7. Vendor Neutrality & Extensions

To preserve vendor neutrality, engine-specific configuration is kept out of the normative standard (see [EXTENSIONS.md](EXTENSIONS.md)): vendor policy files are non-normative and sit at the root of `07-agent/` at the path their tool reads (section 2.2).

Conforming execution engines:
- Rely strictly on the normative files (`START_HERE.md`, `execution-state.json`, `TASK-NNN.json`).
- Safely ignore vendor policy files and `extensions` objects they do not recognise.
- Translate the normative content into vendor-native prompts via execution adapters for the agent runtime in use.

---

## 8. Backward & Forward Compatibility

- **Semantic Versioning**: The specification follows Semantic Versioning (`MAJOR.MINOR.PATCH`).
  - `PATCH` increments denote errata, typo fixes, or schema description updates.
  - `MINOR` increments denote backward-compatible additions (e.g. optional fields in manifest or task packets).
  - `MAJOR` increments denote breaking structural schema modifications.
- **Forward Compatibility Rule**: Conformers MUST ignore unrecognized JSON properties unless explicitly marked as mandatory in the schema.
- **Backward Compatibility Rule**: v1.x execution engines MUST continue to parse and execute all valid v1.0 delivery packs.

---

## 9. Adoption & Ecosystem

The Pravetra Universal Delivery Pack Specification is an open standard. It is licensed under the Apache License 2.0 (see [LICENSE](LICENSE) and [NOTICE](NOTICE)); trademarks are not licensed (see [TRADEMARKS.md](TRADEMARKS.md)).

Reference implementations:
- **Specification Generator**: Pravetra Governance Platform (`https://pravetra.yuktelos.com`).
- **Reference Execution Engine**: `pravetra-conductor` (Proprietary Reference Orchestrator CLI & UI by Yuktelos).
