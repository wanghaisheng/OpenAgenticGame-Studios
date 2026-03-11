<!-- input: copied workflow-status wrapper and the repo-local routing model -->
<!-- output: a compatibility note for the copied workflow-status workflow -->
<!-- pos: reference-layer workflow-status compatibility guide -->
# Workflow Status Compatibility Guide

This copied wrapper is retained as upstream reference only.

The active local router and status cues now live in the local workflow layer rather than a separate workflow-status wrapper.

## Local Equivalent

Use:

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/bmm.md`
- `.codex/core/observability.md`

## Local Mapping

- older `workflow-status` behavior maps into local routing plus active change-record context
- copied BMAD status wrappers are not the authoritative local entry

Use this file only when local routing docs are insufficient.
