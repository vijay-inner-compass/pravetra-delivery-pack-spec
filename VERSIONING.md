# Pravetra Universal Delivery Pack Specification: Versioning & Compatibility

**Specification Version**: `1.1.0` (Draft)  
**License**: Apache-2.0 (see [LICENSE](LICENSE))

---

## 1. Versioning Model

The **Pravetra Universal Delivery Pack Specification** adheres strictly to [Semantic Versioning 2.0.0](https://semver.org/) (`MAJOR.MINOR.PATCH`).

The version is recorded in the top-level manifest envelope under the `specVersion` field:
```json
{
  "specVersion": "1.0.0"
}
```

### 1.1 Specification Version Increments
- **`MAJOR` (e.g. 1.0.0 -> 2.0.0)**:
  - Incompatible breaking changes to the normative protocol structure, required schema fields, or directory layout.
  - Removal or structural alteration of existing required sections (`00-manifest/` through `07-agent/`).
  - Changes to the execution state machine transition semantics that prevent older engines from safely orchestrating tasks.
- **`MINOR` (e.g. 1.0.0 -> 1.1.0)**:
  - Backward-compatible additions to normative schemas (e.g., new optional fields in `TASK-NNN.json` or `manifest.json`).
  - New non-breaking conformance profiles or optional capability tags.
  - New standardized extension namespaces.
- **`PATCH` (e.g. 1.0.0 -> 1.0.1)**:
  - Clarifications to prose, typographical corrections, non-normative example additions, or schema description enhancements with zero semantic changes.

---

## 2. Independent Versioning Principle

**The Specification version is strictly independent of any software product version.**

- The **Delivery Pack Specification** version (e.g. `1.0.0`) governs the data format and interoperability contracts.
- **Pravetra Platform** (e.g. `v2026.10`) is a generator that produces compliant packs.
- **Pravetra Conductor** (e.g. `1.0.0`) is a proprietary execution engine that executes compliant packs.
- Third-party implementations maintain their own independent versioning.

---

## 3. Schema Directory Versioning

JSON Schemas are permanently versioned under versioned URL paths and disk directories:

```text
schemas/
├── v1/
│   ├── delivery-pack-manifest.schema.json
│   ├── task-packet.schema.json
│   ├── execution-state.schema.json
│   ├── policy.schema.json
│   └── artifact.schema.json
└── v2/ (reserved for future breaking releases)
```

Schema IDs use canonical URI prefixes, pinned to the release tag (the URL of a published schema never changes):
`https://raw.githubusercontent.com/vijay-inner-compass/pravetra-delivery-pack-spec/v1.1.0/schemas/v1/<schema-name>.schema.json`

Published schemas within a `MAJOR` series are immutable. In-place breaking schema mutations are strictly prohibited.

---

## 4. Forward and Backward Compatibility Rules

### 4.1 Forward Compatibility (Consumer Responsibility)
- **Unknown Fields Rule**: Conforming execution engines and parsers **MUST NOT fail** when encountering unrecognized properties in JSON manifests, task packets, or execution states. Unrecognized fields must be ignored and preserved where state is round-tripped.
- **Unknown Extensions Rule**: Consumers encountering unrecognized vendor policy files under `07-agent/` or unhandled keys in `extensions` namespaces **MUST safely ignore** them.

### 4.2 Backward Compatibility (Generator Responsibility)
- Generators producing Delivery Packs conforming to specification version `1.x` must ensure all required fields defined in `1.0.0` remain populated.
- Older valid delivery packs (`1.0.0`) must continue to parse and execute successfully on newer `1.x` execution engines.

---

## 5. Deprecation Policy

When a feature, schema field, or directory convention is slated for retirement:
1. It is marked as `deprecated: true` in the JSON Schema and noted in `CHANGELOG.md` in a `MINOR` release.
2. It remains supported by conforming implementations for a minimum deprecation window of **12 months** or until the next `MAJOR` version.
3. It may only be removed upon a `MAJOR` version increment (e.g. `2.0.0`).
