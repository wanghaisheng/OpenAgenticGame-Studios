<!-- input: upstream archive best practices and the repo-local archive model -->
<!-- output: a compatibility note for readers opening the copied archive best-practices guide -->
<!-- pos: reference-layer archive best-practices compatibility guide -->
# Archive Best Practices Compatibility Guide

This copied guide is retained for upstream background only.

The active local archive and closeout flow is:

- `.codex/workflows/archive.md`
- `.codex/core/closeout-loop.md`
- `.codex/core/openspec-sync.md`

## Local Mapping

- copied `_bmad-output/...` archive examples are legacy only
- new non-trivial work should close against `openspec/changes/<change-name>/`
- lessons and follow-up cleanup should feed into `.codex/LESSONS-LEARNED.md` and `.codex/workflows/hygiene.md`

Use this copied guide only when the local archive docs are not enough.
