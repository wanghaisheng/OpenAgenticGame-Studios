<!-- input: copied upstream intelligent-router workflow guidance and the repo-local routing model -->
<!-- output: a compatibility note for readers opening the copied workflow router guide -->
<!-- pos: reference-layer workflow router compatibility guide -->
# Workflow Router Compatibility Guide

This copied guide is kept for upstream intelligent-router context.

The active local router is:

- `.codex/workflows/router.md`

## Local Rule

The repository exposes only two user-facing modes:

- `Quick`
- `BMM`

Anything else in the local workflow layer is supporting infrastructure.

## Supporting Local Docs

- `.codex/core/task-sizing.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/milestone-design.md`
- `.codex/core/harness.md`

## Legacy Mapping

- `Quick Dev` -> local `Quick`
- large planning flows -> local `BMM`
- copied router aliases remain historical context, not the active local router
