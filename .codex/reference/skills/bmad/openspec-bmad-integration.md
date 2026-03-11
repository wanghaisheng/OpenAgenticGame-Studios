<!-- input: upstream OpenSpec and BMAD integration guidance and the repo-local BMAD workflow model -->
<!-- output: a compatibility note for readers opening the copied integration skill guide -->
<!-- pos: reference-layer OpenSpec BMAD integration skill compatibility guide -->
# OpenSpec Integration Skill Compatibility Guide

This copied guide is not the local execution authority for this repository.

The repo-local integration layer has been reduced to two user-facing modes:

- `Quick`
- `BMM`

## Local Source Of Truth

Use these first:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`
- `.codex/core/openspec-sync.md`

## Local Translation

- copied BMAD role documents -> upstream background only
- `Quick Dev` -> local `Quick`
- spec-first or discovery-heavy flow -> local `BMM`
- `_bmad-output/...` -> legacy only

Use this file only for upstream context that the local docs do not already summarize.
