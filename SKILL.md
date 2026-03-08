---
name: keep-project-focus
description: Use when a multi-project workflow needs one authoritative current project, especially if create, switch, delete, or proposal-formalization flows leave stale discussion, wrong next actions, or abandoned work still appearing active.
---

# Keep Project Focus

## Overview
Treat current project focus as durable state, not as text inference. Keep one authoritative field and derive orchestration, UI, and next actions from it first.

## Core Pattern
- Store the current project in one durable field such as `settings.focusedProjectId`.
- Read that field first everywhere that needs the active project.
- Update it on create, switch, delete, and proposal formalization.
- Rewrite human-facing `Next Action` text from the authoritative focused project instead of using freeform text as the source of truth.

## Quick Reference
- **Create project**: mark the previous focused project as abandoned when appropriate, append the new project, set focus to the new project, rewrite `Next Action`.
- **Switch project**: set the focused project id first, then regenerate `Next Action` for the chosen project.
- **Delete focused project**: remove the project, select the next valid project or clear focus, then rewrite `Next Action`.
- **Formalize proposal**: remap the old proposal id to the real project id so focus is preserved.

## Common Mistakes
- Inferring the active project from `consensus.md` or similar freeform text.
- Updating banners or cards without updating the durable focus field.
- Forgetting to remap focus when a proposal id changes into a real project id.
- Leaving an abandoned project visible as the effective current project.

## Example
Use when the user says: ???????????????, ????????????????, or ?????????????.
