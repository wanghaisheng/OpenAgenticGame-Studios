<!-- input: upstream beginner guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied beginner guide -->
<!-- pos: reference-layer beginner compatibility guide -->
# Beginner Compatibility Guide

This copied beginner guide is kept only for historical and upstream context.

In this repository, new work should start from:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`

## Local Mode Mapping

If the older guide says:

- `Quick Dev`, read it as local `Quick`
- `quick-spec` or spec-first flow, read it as local `BMM`
- `_bmad-output/changes/...`, read it as a legacy path instead of the preferred local path

## Current Local Paths

The active local user-facing modes are:

- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`

The stronger internal execution rules live in:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/closeout-loop.md`

## Preferred Change Record Path

For new non-trivial work, prefer:

- `openspec/changes/<change-name>/`

Use this copied guide only when the lightweight local workflow docs are not enough.
