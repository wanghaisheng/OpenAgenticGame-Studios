<!-- input: upstream OpenSpec and BMAD workflow integration concepts and the repo-local execution model -->
<!-- output: a compatibility note for readers opening the copied workflow integration guide -->
<!-- pos: reference-layer workflow integration compatibility guide -->
# Workflow Integration Compatibility Guide

This copied guide is kept for upstream workflow background.

The current local workflow integration lives under `.codex/workflows/` and `.codex/core/`.

## Active Local Entrypoints

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`

## Active Local Integration Rules

- milestone design: `.codex/core/milestone-design.md`
- work breakdown: `.codex/core/work-breakdown.md`
- openspec sync: `.codex/core/openspec-sync.md`
- validation and hard gates: `.codex/core/validation-matrix.md` and `.codex/core/executable-guardrails.md`

## Legacy Mapping

- `Quick Dev` -> local `Quick`
- `_bmad-output/changes/...` -> legacy path
- `_bmad/...` -> upstream asset path

Use this file only when the local workflow docs are not enough.
