---
name: project-memory-auditor
description: Use this skill when a project has persistent memory files and you need to validate scope, project rules, changelog, technical decisions, open issues, or conflicts before editing code.
version: 1.0.0
status: official
category: core
---

# Project Memory Auditor

## Purpose

Audit a project's persistent memory before any relevant work.

## When to use

Use when:

- starting work on an existing project
- renaming a project folder
- cleaning repository scope
- preparing a commit
- checking whether a task belongs to the active project
- resolving conflicts between user request, memory, and code

## Process

1. Identify active project.
2. Read project rule file, such as `GEMINI.md`, `AGENTS.md`, or equivalent.
3. Read local memory, usually `/ai-memory`.
4. Read global workspace memory if relevant.
5. Inspect Git status.
6. Detect conflicts.
7. Report what is safe to change.
8. Update memory only if requested or if the task includes memory maintenance.

## Output

Return:

- active project
- rule files found
- memory files found
- conflicts
- Git scope status
- safe next action
