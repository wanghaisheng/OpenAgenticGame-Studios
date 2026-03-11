<!-- input: upstream PRD-to-OpenSpec quick-flow guidance and the repo-local BMAD workflow model -->
<!-- output: a compatibility note for readers opening the copied PRD quick-flow skill guide -->
<!-- pos: reference-layer PRD quick-flow skill compatibility guide -->
# PRD To OpenSpec Skill Compatibility Guide

This copied guide is no longer the authoritative local execution path.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

The local user-facing model is intentionally smaller:

- `Quick`
- `BMM`

## Local Mapping

Interpret older quick-flow terms this way:

- quick-spec -> local `BMM`
- Quick Dev or quick-dev -> local `Quick`
- `_bmad-output/implementation-artifacts/...` -> legacy path
- `openspec/changes/<change-name>/` -> preferred new path

## Use Local Docs First

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/core/openspec-sync.md`

Use this file only as copied upstream context.
