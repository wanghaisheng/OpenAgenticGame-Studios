<!-- input: copied upstream workflow material and the repo-local harness model -->
<!-- output: a compatibility explainer for the copied workflow directory -->
<!-- pos: reference-layer workflow README -->
# Workflow Reference README

This directory is a local copy of upstream workflow material.

It exists so the repository keeps its BMAD/OpenSpec reference set on disk, but it is no longer the primary execution layer for daily work.

For shared legacy terminology and path translation, use `.codex/reference/LEGACY-MAPPING.md`.

## Current Repository Model

User-facing mode selection is intentionally small:

- `Quick`
- `BMM`

Everything else in the local harness is internal support:

- `.codex/core/`
- `.codex/maps/`
- `.codex/templates/`

## What This Folder Still Helps With

- reading upstream terminology
- understanding where older aliases like `@dev` or `@spec` came from
- checking copied workflow details that were intentionally not duplicated into the local execution layer

## What This Folder Does Not Control

This folder does not define:

- current mode routing
- current validation rules
- current milestone design rules
- current change-record truth source

Those live under `.codex/`.

## Legacy Path Note

Many copied files here still refer to:

- `_bmad/...`
- `_bmad-output/changes/...`
- `Quick Dev`

Read those as upstream or historical references unless a repo-local doc explicitly adopts them.
