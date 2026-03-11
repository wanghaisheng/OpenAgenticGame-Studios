<!-- input: upstream PRD-to-OpenSpec quick-flow guidance and the repo-local workflow model -->
<!-- output: a compatibility note for readers opening the copied PRD quick-flow guide -->
<!-- pos: reference-layer PRD quick-flow compatibility guide -->
# PRD To OpenSpec Compatibility Guide

This copied guide is retained for historical background only.

For this repository, PRD-driven work now starts from:

- `AGENTS.md`
- `.codex/README.md`
- `.codex/workflows/router.md`

## Local Routing

Translate the older quick-flow language this way:

- `@workflow-quick-spec` or quick-spec flow -> local `BMM`
- `@workflow-quick-dev` or Quick Dev flow -> local `Quick`
- `_bmad-output/...` references -> legacy only

## Preferred Local Flow

For a PRD-backed change:

1. create or update `openspec/changes/<change-name>/`
2. route through `.codex/workflows/bmm.md` when discovery or planning is still needed
3. route through `.codex/workflows/quick.md` when the milestone is already clear and implementation-ready
4. close through `.codex/workflows/validate.md` and `.codex/workflows/archive.md` when a durable record is needed

## Local Support Rules

- milestone design: `.codex/core/milestone-design.md`
- work breakdown: `.codex/core/work-breakdown.md`
- openspec sync: `.codex/core/openspec-sync.md`
- hard gates: `.codex/core/validation-matrix.md`

Use this copied guide only when the local workflow docs are not enough.
