<!-- input: copied @validate alias semantics and the repo-local workflow model -->
<!-- output: a compatibility note for the copied @validate alias -->
<!-- pos: reference-layer @validate compatibility alias -->
# `@validate` Compatibility Note

This copied alias remains available for historical prompt compatibility.

In this repository, the active validation workflow is:

- `.codex/workflows/validate.md`

## Local Interpretation

- validation is a support workflow, not a primary user-facing mode
- current hard gates live under `.codex/core/validation-matrix.md` and `.codex/core/executable-guardrails.md`
- new work should not assume `_bmad-output/changes/...` as the primary validation target

Use the repo-local workflow docs for current validation behavior.
