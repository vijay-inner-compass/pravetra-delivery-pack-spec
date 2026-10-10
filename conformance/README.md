# Pravetra Universal Delivery Pack Specification: Conformance Test Suite

**Specification Version**: `1.1.0` (Draft)

---

## 1. Overview

This directory provides automated test vectors for validating implementations against the **Pravetra Universal Delivery Pack Specification v1.0**.

Every compliant delivery pack parser, validator, or execution engine MUST pass these test vectors:
- **`valid/`**: Packages that must parse and validate successfully against JSON Schemas v1.
- **`invalid/`**: Intentionally malformed packages that must be rejected with specific, documented validation errors.

---

## 2. Test Vector Matrix

Each vector is validated against the schema named in its `$comment` (manifest, task packet or execution state). Pack-level vectors are complete packs and are validated end to end.

### 2.1 Valid Test Vectors
| Vector ID | Profile Target | Location | Expected Behavior | Status |
|---|---|---|---|:---:|
| `vector-core-001` | `DeliveryPack.Core` | `valid/vector-core-001.json` | A manifest alone: validates against `delivery-pack-manifest.schema.json` (its `integrity.hash` is a placeholder, since there are no files to hash). | Active |
| `vector-core-pack-001` | `DeliveryPack.Core` | `examples/minimal/` | A complete pack: manifest, integrity hash and the Core sections validate. | Active |
| `vector-execution-001` | `DeliveryPack.Execution` | `test-vectors/dp-2026-001/` | A complete pack: dependency graph, atomic `TASK-001.json` and `TASK-002.json`, argument-array commands, execution checkpoint, true integrity hash. | Active |
| `vector-governance-001` | `DeliveryPack.Governance` | `examples/governed/` | A complete pack with quality and ops sections and a true integrity hash. | Active |

### 2.2 Invalid Test Vectors (`conformance/invalid/`)
| Vector ID | Validated against | Targeted Invalidation | Expected Failure Reason | Status |
|---|---|---|---|:---:|
| `err-missing-specversion` | manifest schema | Missing `specVersion` in manifest | Schema validation error: required property `specVersion` not found. | Active |
| `err-path-traversal` | task-packet schema | Task target scope contains `../../etc/shadow` | Security error: path traversal attempts outside workspace root MUST be rejected. | Active |
| `err-shell-interpolation` | task-packet schema | Task command `executable` is a shell string | Security error: shell interpolation prohibited; requires executable + argument array. | Active |
| `err-dependson-malformed` | task-packet schema | `dependsOn` has a non-task id and a duplicate | Schema error: pattern and uniqueness. | Active |
| `err-unsupported-version` | manifest schema | Manifest has `specVersion: "99.0.0"` | Version error: unsupported major specification version. | [Planned] |
| `err-cyclic-dependency` | pack | `TASK-001` depends on `TASK-002`, `TASK-002` depends on `TASK-001` | Graph validation error: cyclical dependency detected. | [Planned] |

## 3. Running Conformance Tests

Conforming validators can execute against this directory:

```bash
# Example test invocation using delivery pack validator (planned CLI package)
# npx <delivery-pack-validator>  (no validator package is published yet) --test-suite ./conformance/
```
