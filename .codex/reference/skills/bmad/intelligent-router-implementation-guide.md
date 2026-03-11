<!-- input: copied upstream intelligent-router guidance and the repo-local routing model -->
<!-- output: a compatibility note for readers opening the copied router implementation guide -->
<!-- pos: reference-layer router compatibility guide -->
# Intelligent Router Compatibility Guide

This copied guide is kept for upstream routing ideas.

The active local router is:

- `.codex/workflows/router.md`

## Local Router Model

The local router makes one user-facing decision:

- `Quick`
- `BMM`

Support workflows such as `review`, `validate`, `archive`, and `hygiene` are invoked inside the chosen mode context, not as extra user-facing modes.

## Local Routing Inputs

The local decision is informed by:

- `.codex/core/task-sizing.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/milestone-design.md`

## Legacy Mapping

- older references to `Quick Dev` map to `Quick`
- older references to broader BMAD mode routing map to `BMM` plus local support workflows

Use this file for upstream context only.
