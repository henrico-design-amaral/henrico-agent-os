---
name: mcp-evaluator
description: Use this skill before installing, enabling, or recommending any MCP server. It evaluates utility, permissions, data exposure, security risk, and project fit.
version: 1.0.0
status: draft
category: mcp
---

# MCP Evaluator

## Purpose

Evaluate MCP servers before installation or use.

## Process

1. Identify MCP source and maintainer.
2. Check purpose.
3. Check required permissions.
4. Check filesystem access.
5. Check network access.
6. Check authentication.
7. Check secrets handling.
8. Check whether it is needed for the current workflow.
9. Prefer least-privilege configuration.
10. Document decision in `mcps/`.

## Output

Return:

- approve/reject/candidate
- reason
- required permissions
- risks
- safer alternative
- rollback plan
