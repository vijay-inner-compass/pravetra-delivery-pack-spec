# Pravetra Universal Delivery Pack Specification: Extension Guide

**Specification Version**: `1.1.0` (Draft)  
**License**: Apache-2.0 (see [LICENSE](LICENSE))  

---

## 1. Principle of Vendor Neutrality

The **Universal Delivery Pack Specification** is intentionally designed as an open, vendor-neutral standard for governing autonomous software delivery.

To ensure long-term durability and avoid coupling to any single AI provider or execution runtime:
1. **Normative Standard**: Machine-readable contracts, schemas, security boundaries, and execution states are vendor-agnostic and standard across all engines.
2. **Non-Normative Extensions**: Vendor-specific prompt formats, CLI instruction files, and proprietary IDE configurations reside strictly in isolated extension directories.

---

## 2. Extension Layout

Vendor-specific policy files are **non-normative** and sit at the root of `07-agent/`, each at the relative path its tool reads, so that copying `07-agent/` into a repository root installs them:

```
07-agent/
├── START_HERE.md                     # [Normative] Agent briefing & operating rules
├── execution-state.json              # [Normative] Checkpoint state machine
├── AGENTS.md                         # [Non-Normative] AGENTS.md convention (Codex and others)
├── CLAUDE.md, .claude/skills/        # [Non-Normative] Anthropic Claude Code
├── GEMINI.md                         # [Non-Normative] Google Gemini CLI
├── .github/copilot-instructions.md   # [Non-Normative] GitHub Copilot
├── .cursor/rules/                    # [Non-Normative] Cursor
└── ...                               # other tools likewise
```

An earlier draft used `07-agent/extensions/<vendor>/`. That layout is not used by the reference generator and is not required; a generator that prefers it may place files there, and consumers ignore both.

Generator-specific data inside JSON files goes in an `extensions` object keyed by vendor (for example `extensions.pravetra` in `execution-state.json`), never in a normative field.

---

## 3. Semantic Mapping Between Standard and Vendor Adapters

Execution engines and adapters translate the normative specification into agent-specific representations using the following mapping:

| Normative Specification Asset | Vendor Translation Target | Example Mapping / Behavior |
|---|---|---|
| `07-agent/START_HERE.md` | Primary System Prompt | Injected as the top-level developer instructions of the agent runtime. |
| `04-delivery/TASK-NNN.json` | Atomic Agent Mission | Read dynamically by the agent runner for each discrete task cycle; `prohibitedChanges` become negative constraints in the runtime's policy file, `allowedCapabilities` map to tool allowlists. |
| `07-agent/execution-state.json` | Checkpoint Memory | Persisted across agent context window compactions or multi-session handoffs. |

---

## 4. Extension Rules and Guardrails

1. **No Relaxation of Constraints**:
   - An extension MUST NOT weaken, override, or contradict constraints defined in `prohibitedChanges`, `securityConstraints`, or `escalateIf`.
2. **Safe Fallback**:
   - Conforming execution engines encountering unrecognized extensions MUST safely ignore them without halting execution or raising fatal errors.
3. **No Hidden State**:
   - Extensions MUST NOT introduce external dependency states not declared in the delivery pack's `01-baseline/` or `04-delivery/TASK-NNN.json`.
4. **Tool Independence**:
   - A delivery pack MUST remain fully executable using the normative files even if every vendor policy file is deleted.
