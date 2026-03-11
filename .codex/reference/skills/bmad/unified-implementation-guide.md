<!-- input: upstream unified BMAD implementation guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied unified BMAD guide -->
<!-- pos: reference-layer unified implementation skill compatibility guide -->
# Unified Implementation Skill Compatibility Guide

This copied guide is not the active execution layer for this repository.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

The local workflow was intentionally simplified so the user only sees:

- `Quick`
- `BMM`

## Start From Local Docs

Use these before any copied upstream reference:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`

## Local Translation

Interpret older terminology this way:

- `Quick Dev` -> local `Quick`
- spec-heavy or discovery-first flow -> local `BMM`
- `_bmad-output/changes/...` -> legacy path
- `openspec/changes/...` -> preferred new path

The repo-local harness and validation model lives under `.codex/core/`.

Use this file only as compatibility background.
