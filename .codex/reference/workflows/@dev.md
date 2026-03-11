<!-- input: copied @dev alias semantics and the repo-local workflow model -->
<!-- output: a compatibility note for the copied @dev alias -->
<!-- pos: reference-layer @dev compatibility alias -->
# `@dev` Compatibility Note

This copied alias remains available for historical prompt compatibility.

In this repository, `@dev` maps to:

- `.codex/workflows/dev.md`

And that file is only a compatibility alias for:

- `.codex/workflows/quick.md`

## Local Interpretation

- `@dev` does not define a separate mode
- `Quick Dev` maps to local `Quick`
- current validation, milestone, and guardrail rules live under `.codex/core/`

If you need current behavior, read `.codex/workflows/quick.md` instead of this reference alias.
