# Coding Agent Instruction Files, Skills & Deliverables Guide

## Researched Registry of Coding Agents & Instruction Files

Researched 20 September 2026. Below is a broad list of coding agents with documented instruction files; it is not an exhaustive registry of every available agent.
Format: Agent : Instruction file : What it does : Location
Paths are relative to your project root unless starting with ~/, which means your home directory. Agent names link to the documentation.
[OpenAI Codex](https://developers.openai.com/codex/guides/agents-md) : AGENTS.md, AGENTS.override.md : Coding conventions, commands, and project guidance : Project root and relevant subdirectories; global ~/.codex/AGENTS.md.
[Claude Code](https://code.claude.com/docs/en/memory) : CLAUDE.md : Persistent project instructions and workflow guidance : CLAUDE.md or .claude/CLAUDE.md; global ~/.claude/CLAUDE.md; modular rules in .claude/rules/*.md.
[Cursor](https://cursor.com/docs/rules) : *.mdc, AGENTS.md : Project rules and instructions scoped to files or tasks : .cursor/rules/*.mdc or project AGENTS.md.
[GitHub Copilot](https://code.visualstudio.com/docs/agent-customization/custom-instructions) : copilot-instructions.md, *.instructions.md : Repository-wide and file-specific coding instructions : .github/copilot-instructions.md and .github/instructions/*.instructions.md; support varies by Copilot surface.
[Gemini CLI](https://geminicli.com/docs/cli/gemini-md/) : GEMINI.md : Project context, coding style, and persistent instructions : Project and relevant directory hierarchy; global ~/.gemini/GEMINI.md.
[Google Antigravity](https://www.antigravity.google/docs/rules-workflows/) : *.md, GEMINI.md : Workspace rules and global preferences : .agents/rules/*.md; global ~/.gemini/GEMINI.md; older .agent/rules/ remains supported.
[Google Jules](https://jules.google/docs) : AGENTS.md : Repository guidance for planning and implementing changes : Project root.
[Windsurf / Devin Desktop](https://docs.devin.ai/desktop/cascade/memories) : *.md, AGENTS.md : Cascade coding rules and workspace guidance : .devin/rules/*.md; older .windsurf/rules/*.md supported; AGENTS.md in project directories.
[Cline](https://github.com/cline/cline/blob/main/docs/customization/cline-rules.mdx) : Markdown rule files : Coding standards, constraints, and project workflows : .clinerules/ or .cline/rules/; global macOS/Linux ~/Documents/Cline/Rules/.
[Roo Code](https://roocodeinc.github.io/Roo-Code/features/custom-instructions/) : *.md, *.txt, AGENTS.md : General and mode-specific instructions : .roo/rules/, .roo/rules-code/, or root AGENTS.md; global ~/.roo/rules/.
[Kilo Code](https://kilo.ai/docs/customize/custom-rules) : Markdown files referenced by kilo.jsonc : Project and global coding rules : Typically .kilo/rules/*.md, registered in the instructions array; older .kilocode/rules/ supported.
[OpenCode](https://opencode.ai/docs/rules/) : AGENTS.md : Persistent coding conventions and project instructions : Project root; global ~/.config/opencode/AGENTS.md.
[Amp](https://ampcode.com/docs/customize/agents-md) : AGENTS.md : Architecture, build/test commands, and conventions : Current directory, parents, and subdirectories; global ~/.config/amp/AGENTS.md.
[Factory Droid](https://docs.factory.ai/harness/agents-md) : AGENTS.md : Project guidance, commands, and working conventions : Project root and subdirectories, including .factory/; global ~/.factory/AGENTS.md.
[JetBrains Junie CLI](https://junie.jetbrains.com/docs/guidelines-and-memory.html) : AGENTS.md : Persistent project guidelines : .junie/AGENTS.md or root AGENTS.md; legacy .junie/guidelines.md supported.
[Kiro](https://kiro.dev/docs/web/steering) : Steering Markdown files : Product context, architecture, coding standards, and testing guidance : .kiro/steering/*.md.
[Continue](https://docs.continue.dev/customize/deep-dives/rules) : *.md : Instructions for Agent, Chat, and Edit modes : .continue/rules/*.md.
[Aider](https://aider.chat/docs/usage/conventions.html) : Any chosen Markdown file, commonly CONVENTIONS.md : Coding conventions supplied as read-only context : Any location; explicitly load with --read CONVENTIONS.md or configure read in .aider.conf.yml.
[Zed Agent](https://zed.dev/docs/ai/instructions) : AGENTS.md : Always-on project and personal instructions : Project root; global ~/.config/zed/AGENTS.md; older .rules and other compatible filenames also supported.
[Warp](https://docs.warp.dev/agents/capabilities/rules/) : AGENTS.md : Project rules and directory-specific guidance : Project root and subdirectories; legacy WARP.md remains supported.
[Replit Agent](https://docs.replit.com/features/project-setup/replit-dot-md) : replit.md : Project context, preferences, and coding guidance : Project root.

---

## Best Practices for Agent Instruction & Rule Files

### 1. Single Canonical Policy with Multi-Target Adapters
- **Principle**: Do not maintain divergent copies of engineering rules by hand. Author a single canonical policy model and render vendor-specific adapter files into deliverables (`07-agent/` in Pravetra Delivery Packs).
- **Format Consistency**: Ensure the canonical version label (e.g. `blueprint-vX-tasks-Y`) is embedded identically in all rendered target files (Codex, Claude, Copilot, Cursor, Gemini, Devin, Cline, Roo, Kilo, Kiro, Continue, Aider, Replit, Zed, Warp).

### 2. Hierarchical Context Scoping
- **Global Context**: Place cross-cutting constraints (e.g., security policies, test execution requirements) in repository root files (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `copilot-instructions.md`).
- **Path-Specific Rules**: Use targeted globbing (such as Cursor `.mdc` frontmatter or `.github/instructions/*.instructions.md`) to apply rules only when matching specific subsystems (e.g. backend services vs. frontend UI).

### 3. Skills Packaging and Modular Workflows
- **On-Demand Loading**: Group specialized domain procedures (e.g. database migrations, security scans, OpenAPI schema sync) into modular skill files located in `.claude/skills/`, `.agents/skills/`, or `.roo/rules/`.
- **Deterministic Action Boundaries**: Clearly demarcate allowed modification paths and prohibited modifications (e.g., prohibiting direct edits to `.git/**` or immutable lock files).

### 4. Verification and Definition of Done
- **Executable Validation**: Every agent instruction file should explicitly declare the build and test commands necessary to verify changes (e.g., `dotnet test`).
- **Escalation Rules**: Mandate that agents halt and escalate rather than inventing architectural patterns or database models when encountering underspecified requirements.