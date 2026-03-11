<!-- input: copied dev-story wrapper and the repo-local BMM workflow model -->
<!-- output: a compatibility note for the copied dev-story workflow -->
<!-- pos: reference-layer dev-story compatibility guide -->
# Dev Story Compatibility Guide

This copied `dev-story` wrapper is retained as upstream BMAD reference.

In this repository, story-level implementation work is handled inside local `BMM`, not as a separate user-facing mode.

## Local Equivalent

Use:

- `.codex/workflows/bmm.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/milestone-design.md`
- `.codex/workflows/review.md`
- `.codex/workflows/validate.md`

## Local Mapping

- older story wrappers map into local BMM milestone execution
- `@workflow-dev-story` is historical alias language, not the preferred local entry
- `_bmad-output/changes/...` references are legacy only

Use this copied file only when local BMM docs are insufficient.
