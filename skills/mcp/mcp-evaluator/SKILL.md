---
name: mcp-evaluator
description: Evaluates new MCP servers for security, utility, and configuration requirements.
---

# MCP Evaluator

Framework for vetting and integrating new Model Context Protocol servers.

## Instructions

1. **Inspect**: Read documentation and source code (if available) for the new MCP.
2. **Audit**: Perform a security review using the template in `templates/mcp-template/MCP-REVIEW.md`.
3. **Test**: (In a safe environment) verify that tools work as expected.
4. **Register**: Add the findings to `registry/mcps-index.md`.

## Constraints

- Never install an MCP without a recorded review.
