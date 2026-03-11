<!-- input: upstream unified implementation guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied unified guide -->
<!-- pos: reference-layer unified implementation compatibility guide -->
# Unified Implementation Compatibility Guide

This copied unified guide is preserved for historical background.

The active local implementation model is no longer a separate unified workflow. It is:

- `Quick` for scoped, clear work
- `BMM` for discovery, planning, and larger or unclear work

## Active Local Entrypoints

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`

## Local Integration Rules

The repo-local workflow glue now lives in:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/openspec-sync.md`
- `.codex/core/closeout-loop.md`

## Legacy Mapping

- `unified workflow` -> local router plus Quick/BMM
- `Quick Dev` -> local `Quick`
- `_bmad-output/changes/...` -> legacy path

Use this copied guide only when you need upstream context that the local docs do not already cover.
