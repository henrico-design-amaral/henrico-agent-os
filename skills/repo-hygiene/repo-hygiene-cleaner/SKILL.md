---
name: repo-hygiene-cleaner
description: Identifies and removes out-of-scope files (e.g., external skills, agents) from product repositories.
---

# Repo Hygiene Cleaner

Ensures that product repositories (Portfolio, LavaPro, etc.) contain only relevant code and local documentation.

## Instructions

1. **Identify**: Search for common out-of-scope folders like `_agents/`, `skills/`, or external repositories.
2. **Verify**: Check `.gitignore` to see if they are intentionally blocked.
3. **Action**: Propose moving them to `Henrico-Agent-OS` or a quarantine folder.
4. **Clean**: Update `.gitignore` to prevent re-entry.

## Constraints

- Never delete files without confirming they are backed up or moved.
