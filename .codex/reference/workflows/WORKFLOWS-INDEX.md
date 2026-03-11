<!-- input: copied upstream workflow names and the repo-local execution model -->
<!-- output: a compatibility index for readers entering the copied workflow reference layer -->
<!-- pos: reference-layer workflow index -->
# Workflow Reference Index

This file is a compatibility index for the copied upstream BMAD workflow set.

It is not the active execution router for this repository.

For the shared legacy translation table, use `.codex/reference/LEGACY-MAPPING.md`.

## Active Local Entrypoints

Use these first:

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`

## How To Read This Folder

Treat the files here as one of three categories:

- upstream workflow references
- historical compatibility notes
- raw copied material that may still mention legacy `_bmad` or `_bmad-output` paths

## Local Interpretation Rules

- `Quick Dev` in copied upstream docs maps to local `Quick`
- `Spec First` or larger BMAD planning flows map to local `BMM`
- new change records should use `openspec/changes/{change-name}/`
- `_bmad-output/changes/` is legacy only

## Recommended Reference Files

Use these when you need extra upstream context:

- `@dev.md`
- `@spec.md`
- `@review.md`
- `@validate.md`
- `bmad-workflow-quick-dev.md`
- `bmad-workflow-quick-spec.md`
- `bmad-workflow-code-review.md`
- `bmad-workflow-check-compliance.md`

If a copied reference conflicts with `.codex/workflows/` or `.codex/core/`, follow the repo-local docs.
