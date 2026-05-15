---
name: design-system-auditor
description: Validates UI implementation against the established design system tokens and principles.
---

# Design System Auditor

Ensures that all styles and components adhere to the project's design system (e.g., Onyx & Gilded).

## Instructions

1. **Scan**: Inspect HTML and CSS for hardcoded values.
2. **Compare**: Check against tokens in `ai-memory/03-design-system.md` or `tailwind.config`.
3. **Correct**: Propose replacing ad-hoc styles with system-defined utilities.

## Constraints

- Preserve accessibility (WCAG 2.2) above all else.
