# Pravetra Universal Delivery Pack Specification: Conformance Guide

**Specification Version**: `1.1.0` (Draft)  
**License**: Apache-2.0 (see [LICENSE](LICENSE))  
**Canonical Repository**: [https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec](https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec)  

---

## 1. Overview

This document defines the formal conformance levels, verification criteria, and compliance testing procedures for the **Universal Delivery Pack Specification v1.0**. 

Conformance allows software generators (such as the Pravetra governance platform, architectural modeling tools, and custom enterprise pipelines) and execution consumers (such as `pravetra-conductor`, CI/CD runners, and autonomous agent adapters) to establish an unambiguous, vendor-neutral interoperability contract.

An implementation may claim conformance to one of four hierarchical profiles:
1. **Delivery Pack Core (`DeliveryPack.Core`)**
2. **Delivery Pack Execution (`DeliveryPack.Execution`)**
3. **Delivery Pack Governance (`DeliveryPack.Governance`)**
4. **Delivery Pack Full (`DeliveryPack.Full`)**

---

## 2. Conformance Profiles

```
┌────────────────────────────────────────────────────────┐
│             LEVEL 4: DeliveryPack.Full                 │
│  Governance + Domain Models + Visual HTML Viewers +    │
│  Strict Commercial Isolation (08-commercial/)          │
└───────────────────────────▲────────────────────────────┘
                            │
┌───────────────────────────┴────────────────────────────┐
│           LEVEL 3: DeliveryPack.Governance             │
│  Execution + Quality Matrix (05-quality/) +            │
│  Ops Runbooks (06-ops/) + SHA-256 Integrity Hashes     │
└───────────────────────────▲────────────────────────────┘
                            │
┌───────────────────────────┴────────────────────────────┐
│           LEVEL 2: DeliveryPack.Execution              │
│  Core + Atomic Task Packets (TASK-NNN.json) +          │
│  Execution State Machine + Normative Agent Policies    │
└───────────────────────────▲────────────────────────────┘
                            │
┌───────────────────────────┴────────────────────────────┐
│             LEVEL 1: DeliveryPack.Core                 │
│  Protocol Manifest Envelope + Baseline Pin +           │
│  System Context + High-Level Architecture (HLD)        │
└────────────────────────────────────────────────────────┘
```

### 2.1 Level 1: Delivery Pack Core (`DeliveryPack.Core`)
The **Core** profile represents the minimum viable architectural handoff. It captures the project baseline, system scope, and high-level technical decisions without prescribing machine-executable agent tasks.

- **Target Systems**: Read-only architecture viewers, documentation portals, compliance cataloging tools.
- **Mandatory Files & Sections**:
  - `00-manifest/MANIFEST.md` or `manifest.json` (validating against `delivery-pack-manifest.schema.json` with `conformanceLevel: "DeliveryPack.Core"`)
  - `01-baseline/baseline-pin.md` (repository commit hash, branch label, or greenfield marker)
  - `02-context/context-summary.md` and `requirements.md`
  - `03-architecture/architecture-summary.md`

### 2.2 Level 2: Delivery Pack Execution (`DeliveryPack.Execution`)
The **Execution** profile extends Core to provide machine-executable task packets and runtime state tracking for autonomous coding agents and CLI runners.

- **Target Systems**: Autonomous coding agents, local orchestrators, and automated CI execution engines.
- **Mandatory Additions**:
  - `00-manifest/manifest.json` declaring `conformanceLevel: "DeliveryPack.Execution"` (or higher), whose `integrity.hash` is true (SPECIFICATION.md section 3.1).
  - `04-delivery/task-list.md`: Dependency-ordered task catalogue.
  - `04-delivery/TASK-NNN.json`: Canonical atomic task packets conforming to `task-packet.schema.json`.
  - `04-delivery/TASK-NNN.md`: Human-readable task descriptions.
  - `07-agent/execution-state.json`: Runtime progress and checkpoint state machine conforming to `execution-state.schema.json`.
  - `07-agent/START_HERE.md`: Base agent briefing and operating rules.
- **Optional (non-normative)**: vendor policy files at the root of `07-agent/` (for example `AGENTS.md` and tool-specific rule files, see SPECIFICATION.md section 2.2). A draft of this profile also listed `07-agent/execution-policy.json`, `07-agent/capabilities.json` and `07-agent/instructions.md`; they are not required in v1.0 and may be added as optional files in a later minor version.

### 2.3 Level 3: Delivery Pack Governance (`DeliveryPack.Governance`)
The **Governance** profile extends Execution by embedding engineering controls, test matrices, operational runbooks, and cryptographic integrity verification.

- **Target Systems**: Regulated enterprise delivery, security-critical systems, financial/healthcare software pipelines, and tamper-evident audit loggers.
- **Mandatory Additions**:
  - `04-delivery/implementation-readiness-report.md`: Formal decision gate readiness report.
  - `05-quality/quality-and-security.md`: Test assertions, coverage baselines, and data classification boundaries.
  - `06-ops/deployment-and-rollback.md`: Pre-deployment checks, deployment commands, health probes, and rollback procedures.
  - **Integrity Envelope**: Top-level manifest must include cryptographic SHA-256 hashes for all pack contents.

### 2.4 Level 4: Delivery Pack Full (`DeliveryPack.Full`)
The **Full** profile represents the complete enterprise delivery asset. It incorporates detailed domain data models, interactive visual HTML viewers, executive decision dossiers, and isolated commercial boundaries.

- **Target Systems**: Full-lifecycle enterprise engineering governance platforms (Pravetra), executive stakeholders, and multi-disciplinary software teams.
- **Mandatory Additions**:
  - `00-manifest/executive-dossier.md` (and `.pdf` / `.html`)
  - `03-architecture/domain-data-model.md` and `domain-data-model.html`: Comprehensive entity-relationship and persistence models.
  - Visual HTML viewers for requirements, architecture, and task packets.
  - **Commercial Boundary Isolation**: If `08-commercial/` is present, it must be listed as strictly protected in the agent policy (`07-agent/START_HERE.md` and the vendor policy files), prohibiting autonomous agent access or modification.

---

## 3. Conformance Matrix

| Requirement / Asset | Core | Execution | Governance | Full |
|---|:---:|:---:|:---:|:---:|
| Protocol Manifest Envelope (`specVersion`, `packId`) | **M** | **M** | **M** | **M** |
| Baseline Pinning (`01-baseline/`) | **M** | **M** | **M** | **M** |
| Context & Requirements (`02-context/`) | **M** | **M** | **M** | **M** |
| Architecture Summary (`03-architecture/`) | **M** | **M** | **M** | **M** |
| Atomic Task Packets (`TASK-NNN.json`) | — | **M** | **M** | **M** |
| Task List & Dependency Graph (`task-list.md`) | — | **M** | **M** | **M** |
| Execution State Machine (`execution-state.json`) | — | **M** | **M** | **M** |
| Normative Agent Contract (`07-agent/`) | — | **M** | **M** | **M** |
| Quality & Security Specification (`05-quality/`) | — | — | **M** | **M** |
| Deployment & Rollback Runbooks (`06-ops/`) | — | — | **M** | **M** |
| Cryptographic Integrity Verification (SHA-256) | — | — | **M** | **M** |
| Executive Decision Dossier (`00-manifest/`) | — | — | — | **M** |
| Domain Data Models (`domain-data-model.md`) | — | — | — | **M** |
| Standalone Visual HTML Viewers | — | — | — | **M** |
| Commercial Section Isolation (`08-commercial/`) | — | — | — | **M*** |

*\* `08-commercial/` is optional; when present in a Full pack, strict agent access restrictions are mandatory.*

---

## 4. Verification and Self-Certification

### 4.1 Generator Verification
A software tool producing delivery packs claims conformance by passing the automated schema and structure validation suite:
```bash
# Validate delivery pack directory against schemas (planned CLI validator package)
# npx <delivery-pack-validator> --path ./my-delivery-pack --level DeliveryPack.Execution
```

### 4.2 Consumer (Execution Engine) Conformance
An execution tool (such as `pravetra-conductor`) claims **Execution Conformance** if it:
1. Validates the top-level manifest protocol envelope and respects `conformanceLevel`.
1a. Recomputes `integrity.hash` as SPECIFICATION.md section 3.1 defines and rejects a pack that does not match.
2. Reads and parses all atomic `TASK-NNN.json` packets in declared dependency order (`sequence` / `dependsOn`).
3. Enforces task boundaries (`targetScope`, `allowedChanges`, `prohibitedChanges`).
4. Executes compilation and test commands using direct argument-array execution (the argument-array form of the language's process API, for example `execFile` in Node.js, `subprocess.run` with a list in Python, `exec.Command` in Go) rather than arbitrary shell string interpolation.
2a. Accepts sub-task ids (`TASK-NNN.N`) and the optional `parentTaskId` (specification 1.1.0): the parent MUST be a task in the pack, the chain of parents MUST NOT loop and a sub-task MUST depend on its parent. A consumer that does not understand `parentTaskId` ignores it and runs the pack by `dependsOn`.
5. Updates and preserves `07-agent/execution-state.json` checkpoints after each completed task.
6. Stops execution and escalates to human review when encountering conditions in `escalateIf` or when `humanApprovalRequired: true`.

---

## 5. Formal Conformance Statement

A conformant generator or executor may publish the following badge or statement in technical documentation:

> **"Conformant with Pravetra Universal Delivery Pack Specification v1.0 (Level: DeliveryPack.Execution)"**
