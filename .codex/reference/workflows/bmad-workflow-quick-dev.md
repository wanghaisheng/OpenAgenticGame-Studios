<!-- input: copied quick-dev workflow wrapper and the repo-local execution model -->
<!-- output: a compatibility note for the copied quick-dev workflow wrapper -->
<!-- pos: reference-layer quick-dev workflow compatibility guide -->
# Quick Dev Workflow Compatibility Guide

This copied wrapper is kept for upstream workflow context.

The active local equivalent is:

- `.codex/workflows/quick.md`

## Local Interpretation

- `quick-dev` maps to local `Quick`
- local validation and guardrails live under `.codex/core/`
- `openspec/changes/{change-name}/` is the preferred local change-record path
- `_bmad-output/changes/...` in copied material is legacy only

## Why This File Still Exists

It is useful when you need to understand the older BMAD wrapper naming, but it is not the active local implementation contract.
