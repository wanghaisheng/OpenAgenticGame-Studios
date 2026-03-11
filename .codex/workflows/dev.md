<!-- input: legacy quick-dev prompts, repository context, and implementation tasks -->
<!-- output: compatibility routing for implementation work -->
<!-- pos: compatibility alias for the Quick workflow -->
# Dev Workflow

This file remains for compatibility with older `@dev` or quick-dev prompts.

In this repository, direct implementation work now lives in:

- `.codex/workflows/quick.md`

## What To Do

1. Follow `quick.md` as the primary implementation workflow.
2. Apply the shared internal rules from:
   - `.codex/core/harness.md`
   - `.codex/core/work-breakdown.md`
   - `.codex/core/task-sizing.md`
   - `.codex/core/milestone-design.md`
   - `.codex/core/validation-matrix.md`
   - `.codex/core/closeout-loop.md`
3. Define one coherent milestone before implementation expands.
4. If the task outgrows Quick or no longer fits one milestone, switch to `.codex/workflows/bmm.md`.

## Compatibility Rule

Keep treating `dev.md` as an alias, not a separate user-facing mode. It inherits the same decomposition, validation, and closeout rules as `quick.md`.
