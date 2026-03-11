<!-- input: copied status-management wrapper and the repo-local workflow model -->
<!-- output: a compatibility note for the copied status-management workflow -->
<!-- pos: reference-layer status-management compatibility guide -->
# Status Management Compatibility Guide

This copied workflow wrapper is upstream reference only.

This repository does not expose status management as a separate user-facing mode.

## Local Equivalent

Status is now reflected through:

- the current Quick or BMM workflow context
- the active change record under `openspec/changes/<change-name>/`
- the repo-local closeout and validation rules under `.codex/core/`

## Local Docs To Use

- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/workflows/validate.md`
- `.codex/core/observability.md`
- `.codex/core/closeout-loop.md`

## Legacy Mapping

- `Quick Dev` -> local `Quick`
- `_bmad-output/...` -> legacy path
- copied status wrapper logic is not the local source of truth
