<!-- input: copied upstream BMAD/OpenSpec terminology and the repo-local workflow model -->
<!-- output: a single compatibility mapping source for the reference layer -->
<!-- pos: reference-layer legacy mapping index -->
# Legacy Mapping

Use this file when older BMAD or OpenSpec reference material uses names or paths that are no longer the active local workflow model.

## Mode Mapping

- `Quick Dev` -> local `Quick`
- spec-first, discovery-heavy, or broader planning flow -> local `BMM`
- old unified router language -> local `.codex/workflows/router.md`

## Path Mapping

- `openspec/changes/<change-name>/` -> preferred path for new non-trivial change records
- older `_bmad-output/...` record paths -> legacy only
- older `_bmad/...` config or workflow paths -> upstream vendor/source material only

## Alias Mapping

- `@dev` -> `.codex/workflows/dev.md` -> compatibility alias for local `Quick`
- `@spec` -> `.codex/workflows/spec.md` -> compatibility alias for local `BMM`
- `@workflow` or `@w` -> `.codex/workflows/router.md`

## Authority Rule

If copied reference material conflicts with repo-local workflow docs, follow:

1. `.codex/workflows/`
2. `.codex/core/`
3. `.codex/maps/`

Use copied reference material only for historical or upstream context.
