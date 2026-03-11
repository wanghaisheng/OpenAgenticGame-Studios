<!-- input: copied @spec alias semantics and the repo-local workflow model -->
<!-- output: a compatibility note for the copied @spec alias -->
<!-- pos: reference-layer @spec compatibility alias -->
# `@spec` Compatibility Note

This copied alias remains available for historical prompt compatibility.

In this repository, `@spec` maps to:

- `.codex/workflows/spec.md`

And that file is only a compatibility alias for:

- `.codex/workflows/bmm.md`

## Local Interpretation

- `@spec` does not define a separate user-facing mode
- new non-trivial change records should use `openspec/changes/{change-name}/`
- `_bmad-output/changes/...` is legacy only

If you need current planning behavior, read `.codex/workflows/bmm.md` instead of this reference alias.
