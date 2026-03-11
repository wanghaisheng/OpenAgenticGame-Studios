<!-- input: upstream Quick Dev implementation guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied BMAD implementation guide -->
<!-- pos: reference-layer Quick implementation skill compatibility guide -->
# Quick Implementation Skill Compatibility Guide

This copied guide is kept for upstream reference only.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

For this repository, the active local implementation path is:

- `.codex/workflows/quick.md`

## Local Mapping

When this older guide mentions:

- `Quick Dev`, use local `Quick`
- `@dev`, read it through `.codex/workflows/dev.md` as a compatibility alias
- `_bmad-output/changes/...`, treat it as legacy rather than preferred

## Local Execution Layer

Quick work here automatically inherits:

- `.codex/core/harness.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/observability.md`

Read this file only when the local workflow docs are not enough.
