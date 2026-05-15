---
name: project-memory-auditor
description: Audits project memory files (README, GEMINI.md, changelog) for consistency and accuracy.
---

# Project Memory Auditor

This skill ensures that all project memory files are up to date and correctly reflect the current state of the repository.

## Instructions

1. **Scan**: Read `README.md`, `GEMINI.md`, and everything in `ai-memory/`.
2. **Verify**: Compare documented state with the actual code and directory structure.
3. **Report**: Highlight any discrepancies or outdated information.
4. **Update**: Propose or apply corrections to maintain the "source of truth".

## Constraints

- Never invent context.
- Always check if a decision is already recorded before adding it.
