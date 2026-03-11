<!-- input: upstream BMAD beginner guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied beginner skill guide -->
<!-- pos: reference-layer beginner skill compatibility guide -->
# Beginner Skill Compatibility Guide

This copied beginner guide is retained as upstream reference only.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

For this repository, the active local entry sequence is:

1. `AGENTS.md`
2. `.codex/README.md`
3. `.codex/workflows/router.md`

## Local Interpretation

Translate older terms this way:

- `Quick Dev` -> local `Quick`
- `quick-spec` or broader planning workflow -> local `BMM`
- `_bmad-output/changes/...` -> legacy path
- `_bmad/...` -> upstream source asset path

## Active Local Workflow Layer

Use these local docs first:

- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/workflows/validate.md`
- `.codex/workflows/archive.md`

The repo-local harness behind those modes lives under `.codex/core/`.

Use this file only for copied upstream background.
