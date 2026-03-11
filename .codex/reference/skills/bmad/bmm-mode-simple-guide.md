<!-- input: upstream BMAD BMM concepts and repo-local workflow decisions -->
<!-- output: a compatibility note for readers looking for the old BMM simple guide -->
<!-- pos: compatibility page in the copied BMAD reference layer -->
# BMM Mode Compatibility Guide

This repository still uses the `BMM` mental model for larger or unclear work that needs framing before or during implementation.

What changed is the execution layer, not the user-facing mode name.

## Active Entrypoint

Use:

- `.codex/workflows/bmm.md`

Do not treat this reference file as the primary execution workflow.

## What Stayed The Same For Users

- `BMM` is still the mode for requirement discovery through implementation.
- Users still use BMM when scope is unclear, cross-cutting, or high-risk.
- The workflow still covers planning, change framing, implementation, validation, and closeout.

## What Changed Internally

`BMM` now automatically relies on repo-local support docs:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/closeout-loop.md`

It also prefers `openspec/changes/{change-name}/` for new change records and uses repo maps for system-specific context.

## Compatibility Notes

- Legacy `@spec` prompts map to `.codex/workflows/spec.md`, which is now a compatibility alias for `bmm.md`.
- `BMM` is still required when a Quick task grows beyond the bounded sizing envelope.
- Use `.codex/reference/` only when upstream BMAD detail is needed beyond the local execution docs.
