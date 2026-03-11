<!-- input: upstream OpenSpec and BMAD integration guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied integration guide -->
<!-- pos: reference-layer OpenSpec BMAD integration compatibility guide -->
# OpenSpec Integration Compatibility Guide

This copied integration guide is kept for upstream background.

The active local integration for this repository lives under:

- `.codex/workflows/`
- `.codex/core/`

## Current Local Integration Points

- routing: `.codex/workflows/router.md`
- scoped implementation: `.codex/workflows/quick.md`
- discovery and planning: `.codex/workflows/bmm.md`
- openspec discipline: `.codex/core/openspec-sync.md`
- milestone planning: `.codex/core/milestone-design.md`
- work breakdown: `.codex/core/work-breakdown.md`

## Legacy Mapping

- older BMAD role and workflow wrappers are copied reference material only
- `Quick Dev` -> local `Quick`
- `_bmad-output/...` -> legacy path
- external `.trae` or `file:///...` links in older copies are not the local source of truth

Use this copied guide only when the local workflow docs do not answer the question.
