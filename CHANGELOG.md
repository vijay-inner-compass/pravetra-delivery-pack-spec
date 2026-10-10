# Universal Delivery Pack Specification: Changelog

All notable changes to the Universal Delivery Pack Specification will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.0] - 2026-10-08

Additive (MINOR, VERSIONING.md section 1.1): every `1.0.0` pack remains valid.

### Added
- **Sub-tasks**: task ids may be `TASK-NNN.N` (the pattern was `TASK-NNN`) in `taskId`, `dependsOn`, `unlocks`, the manifest `tasks` list and the execution-state task entries; files are `TASK-NNN.N.json` / `.md`.
- **`parentTaskId`** (optional, string or null) on task packets and on execution-state task entries: the primary task a sub-task belongs to. Absent on a primary task. The parent must exist in the pack, parents must not loop and a sub-task must depend on its parent (SPECIFICATION.md section 5.1, CONFORMANCE.md section 4.2).
- **`reviewerChecklist`** (optional, string array) on sub-task packets.
- `task-list.md` renders the hierarchy as an indented list when a pack has sub-tasks.

## [Unreleased] - draft amendments before first publication

### Clarified (no schema change, no version bump)
- `sourceRefs[].entityType` stays a free string; the Pravetra generator now also writes the kind `ComponentResponsibility` for a sub-task built from a component's recorded responsibility instead of from a requirement (SPECIFICATION.md section 5.1). No schema enumeration changes, so the specification version is unchanged.
- The layout of the Markdown files (`TASK-NNN.md`, `task-list.md`, `MANIFEST.md`) is non-normative, and `07-agent/COMMON_RULES.md` is an optional, non-normative file for rules shared by every task (SPECIFICATION.md section 2.1). The JSON packets are unchanged: every field and line stays in them.

The specification is still a draft and has not been published, so these tighten v1.0 rather than version it.

### Added
- **Execution state**: an optional `sourceCommit` on each task entry (the commit that holds the task's work), next to the existing `completedAt`.

### Changed
- **`integrity.hash` is defined**: the digest of a checksum text over every file the manifest lists except `manifest.json` (SPECIFICATION.md section 3.1). Consumers verify it.
- **`packId`** is any 3-128 character id of letters, digits, `.`, `_`, `-` (was `DP-YYYY-NNN`).
- **Task packets**: `dependsOn` / `unlocks` items must be `TASK-NNN` ids and unique; `commands` are `{executable, args[], purpose, workingDirectory?}` (the single `command` string is gone); `humanApprovalRequired` is required; `artifactHashes` values and `baseline.commitHash` are hex-pattern checked.
- **Execution state**: `blueprintId` / `blueprintVersion` moved from required top-level fields to the vendor `extensions` object; `dependsOn` items must be task ids.
- **Layout**: vendor policy files sit at the root of `07-agent/`; `execution-policy.json`, `capabilities.json` and `instructions.md` are no longer required by the Execution profile; `START_HERE.md` is the normative briefing.
- Manifest `tasks`, `capabilities`, `policies`, `artifacts` and each section's `files` must be unique; section file paths must be safe relative paths.

### Added
- Complete `test-vectors/dp-2026-001/` and `examples/{minimal,standard,governed}` packs that validate end to end; invalid vectors `err-shell-interpolation` and `err-dependson-malformed`.

## [1.0.0] - 2026-10-06

### Added
- **Top-Level Protocol Envelope**: Added `specVersion`, `packId`, `generator`, `conformanceLevel`, and `integrity` envelope fields to `delivery-pack-manifest.schema.json`.
- **Hierarchical Conformance Profiles**: Defined 4 official conformance levels in `CONFORMANCE.md`:
  - `DeliveryPack.Core` (Level 1)
  - `DeliveryPack.Execution` (Level 2)
  - `DeliveryPack.Governance` (Level 3)
  - `DeliveryPack.Full` (Level 4)
- **Vendor Neutrality & Extension Standard**: Isolated vendor-specific agent configuration into `07-agent/extensions/{anthropic,google,github,cursor}/` and documented semantic mappings in `EXTENSIONS.md`.
- **Atomic Task Packet Formalization**: Expanded `task-packet.schema.json` to include formal `inputs`, `expectedOutputs`, `allowedCapabilities`, `securityConstraints`, `humanApprovalRequired`, and `artifactHashes`.
- **Formal JSON Schemas**: Published JSON Schema Draft 2020-12 specifications under `schemas/v1/`.
- **Test Vectors**: Created reference delivery pack test vectors for automated compliance verification.
