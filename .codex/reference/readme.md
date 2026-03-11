<!-- input: copied upstream BMAD/OpenSpec files and repo-local workflow policy -->
<!-- output: guidance for using the reference layer without confusing it for the active workflow -->
<!-- pos: index for the copied reference material under .codex/reference -->
# Reference Layer

This folder is a local copy of upstream BMAD/OpenSpec material.

It exists for depth and compatibility, not as the primary execution layer for this repository.

For shared legacy terminology and path translation, use `.codex/reference/LEGACY-MAPPING.md`.

## When To Use It

Use `.codex/reference/` only when:

- the lightweight repo-local workflow docs are not enough
- you need upstream BMAD terminology or examples
- you are checking how a copied reference concept maps to the local workflow layer

## When Not To Use It

Do not start from this folder for normal work.

The active execution entrypoints are:

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`

## Interpretation Rule

If copied upstream reference docs conflict with the repo-local workflow layer:

1. follow `.codex/workflows/`, `.codex/core/`, and `.codex/maps/`
2. treat the copied text as historical or upstream context
3. update the local workflow docs intentionally if the repo should adopt the upstream change
