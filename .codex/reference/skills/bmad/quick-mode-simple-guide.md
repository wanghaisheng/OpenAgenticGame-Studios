<!-- input: upstream BMAD quick-mode concepts and repo-local workflow decisions -->
<!-- output: a compatibility note for readers looking for the old Quick simple guide -->
<!-- pos: compatibility page in the copied BMAD reference layer -->
# Quick Mode Compatibility Guide

This repository still uses the `Quick` mental model for small, clear implementation work.

What changed is the execution layer, not the user-facing mode name.

## Active Entrypoint

Use:

- `.codex/workflows/quick.md`

Do not treat this reference file as the primary execution workflow.

## What Stayed The Same For Users

- `Quick` is still the mode for bug fixes, scoped features, and bounded refactors.
- Users still do not need to think about architecture-heavy planning for small tasks.
- The workflow still aims to move from request to implementation quickly.

## What Changed Internally

`Quick` now automatically relies on repo-local support docs:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/closeout-loop.md`

It also uses repo maps when the task touches hot paths such as runtime routing, content generation, or SEO auditing.

## Compatibility Notes

- Legacy `@dev` prompts map to `.codex/workflows/dev.md`, which is now a compatibility alias for `quick.md`.
- If a Quick task grows beyond the sizing envelope, it should escalate to `.codex/workflows/bmm.md`.
- Use `.codex/reference/` only when upstream BMAD detail is needed beyond the local execution docs.
