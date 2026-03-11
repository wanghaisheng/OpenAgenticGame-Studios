<!-- input: copied BMAD skill material and the repo-local Quick/BMM execution model -->
<!-- output: a compatibility explainer for the copied BMAD skill reference set -->
<!-- pos: reference-layer BMAD skill README -->
# BMAD Skill Reference README

This folder contains copied BMAD skill documentation kept for local reference.

It is not the active execution layer for this repository.

For the shared compatibility translation table, use `.codex/reference/LEGACY-MAPPING.md`.

## Local Mapping

Use this mapping when reading older BMAD material:

- `Quick Dev` -> local `Quick`
- spec-led or larger planning flows -> local `BMM`
- `_bmad-output/changes/...` -> legacy path, not the preferred local truth source
- `_bmad/...` -> upstream vendor/source material, not the repo-local workflow layer

## Start Elsewhere First

For current execution, start with:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`

Only come back here when you need extra upstream background.

## High-Value Local Replacements

The repository now has local replacements for the most important execution concerns:

- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`

If a copied BMAD skill says something different from those files, follow the repo-local docs.
