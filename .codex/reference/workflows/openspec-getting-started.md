<!-- input: upstream OpenSpec getting-started guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied OpenSpec getting-started guide -->
<!-- pos: reference-layer OpenSpec getting-started compatibility guide -->
# OpenSpec Getting Started Compatibility Guide

This copied guide remains useful for generic OpenSpec concepts, but it is not the primary local start point.

For this repository, start from:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`

## What Still Applies

These OpenSpec ideas are still valid locally:

- `openspec/specs/` is the long-lived behavior record
- `openspec/changes/<change-name>/` is the preferred home for new non-trivial changes
- `proposal.md`, `design.md`, `tasks.md`, and delta specs still matter

## What Is Repo-Local

This repository adds a stronger local harness around OpenSpec:

- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/core/openspec-sync.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`

## Legacy Mapping

- `_bmad-output/changes/...` -> legacy path
- `Quick Dev` -> local `Quick`
- broader planning or discovery flow -> local `BMM`

Use the full copied OpenSpec reference only when the local workflow docs are not enough.
