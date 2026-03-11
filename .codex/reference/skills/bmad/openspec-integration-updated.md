<!-- input: upstream OpenSpec and BMAD integration concepts and the repo-local execution model -->
<!-- output: a compatibility note for readers opening the copied integration guide -->
<!-- pos: reference-layer OpenSpec integration compatibility guide -->
# OpenSpec Integration Compatibility Guide

This copied guide is kept for upstream context.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

In this repository, the active integration model is simpler and more local:

- users choose only `Quick` or `BMM`
- `.codex/core/` carries the harness rules
- `openspec/changes/{change-name}/` is the preferred change-record path

## Local Replacements

Use these first:

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/core/openspec-sync.md`
- `.codex/core/milestone-design.md`

## How To Read This Guide

Read this file as:

- upstream background on OpenSpec and BMAD integration
- historical context for older aliases and workflow names
- reference material when local docs intentionally stay shorter

Do not read it as the current local implementation contract.

## Local Interpretation Rules

- `Quick Dev` maps to local `Quick`
- `BMM` maps to local `BMM`
- `_bmad-output/changes/...` is legacy only
- `_bmad/...` is upstream source material, not the active repo-local harness
