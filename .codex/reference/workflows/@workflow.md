<!-- input: copied @workflow alias semantics and the repo-local routing model -->
<!-- output: a compatibility note for the copied @workflow alias -->
<!-- pos: reference-layer @workflow compatibility alias -->
# `@workflow` Compatibility Note

This copied alias remains available for historical prompt compatibility.

In this repository, the active router is:

- `.codex/workflows/router.md`

## Local Interpretation

- the local router chooses only between `Quick` and `BMM`
- support workflows such as `review`, `validate`, `archive`, and `hygiene` run inside that chosen mode context
- the larger copied BMAD workflow surface is reference material, not the active local routing contract

If you need current routing behavior, read `.codex/workflows/router.md`.
