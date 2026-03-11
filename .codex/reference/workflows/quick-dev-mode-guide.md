<!-- input: upstream Quick Dev concepts and the repo-local execution model -->
<!-- output: a compatibility note for readers opening the copied Quick Dev guide -->
<!-- pos: reference-layer Quick Dev compatibility guide -->
# Quick Dev Compatibility Guide

This copied guide is kept for historical and upstream context.

In this repository, the active local equivalent is:

- `.codex/workflows/quick.md`

## Local Interpretation

When this older guide says:

- `Quick Dev`, read it as local `Quick`
- `@dev` or quick-dev workflow, read it through `.codex/workflows/dev.md` as a compatibility alias
- `_bmad-output/changes/...`, read it as a legacy path rather than the preferred local path

## Current Local Rules

The current local Quick path is strengthened by:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/executable-guardrails.md`

So the user-facing idea stayed similar, but the execution layer is now stronger and more repo-specific.
