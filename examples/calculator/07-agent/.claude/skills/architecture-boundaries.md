# Architecture Boundaries

> Canonical policy version: blueprint-v2-tasks-26-e1ec194e
> Generated: 2026-10-09 10:18:38Z
> Project: E01-calculator
Decomposition: ModularMonolith.

No existing-system constraints — greenfield architecture choice, revisited as real design work narrows scope. Requirements this architecture must satisfy: The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop. | The calculator shall be available to analysts whenever they work, because it runs locally on their laptop and needs no network or external service. | The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations. | The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database. | The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.

Do not cross a task's own target scope without an explicit, recorded dependency.
