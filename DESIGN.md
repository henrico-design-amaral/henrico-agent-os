# Design Principles — Henrico Agent OS

Guidelines for creating new skills, agents, and workflows to maintain consistency across the ecosystem.

## Skill Design

1. **Atomic**: One skill should do one thing exceptionally well.
2. **Context-Aware**: Must check project memory before acting.
3. **Safe**: Never perform destructive actions without verification.
4. **Verifiable**: Should report exactly what was changed and why.

## Documentation Standard

Every skill must have a `SKILL.md` file following the standard template:
- YAML Metadata
- Clear Instructions
- Examples
- Constraints

## Visual Standard (for UI Agents)

- **Technical**: Minimalist and precise.
- **Editorial**: Strong typography and grid focus.
- **Premium**: Avoid generic templates and placeholders.
