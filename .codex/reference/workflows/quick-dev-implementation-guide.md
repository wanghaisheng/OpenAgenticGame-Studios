<!-- input: upstream Quick Dev implementation guidance and the repo-local execution model -->
<!-- output: a compatibility note for readers opening the copied implementation guide -->
<!-- pos: reference-layer Quick implementation compatibility guide -->
# Quick Implementation Compatibility Guide

This copied implementation guide is not the active execution document for this repository.

The current local equivalent is:

- `.codex/workflows/quick.md`

## What Changed Locally

The older guide describes a lighter `Quick Dev` flow.

In this repository:

- `Quick Dev` maps to local `Quick`
- the user-facing mode stayed small
- the execution layer is strengthened by repo-local harness rules and validation gates

## Local Support Docs

Quick work is reinforced by:

- `.codex/core/harness.md`
- `.codex/core/task-sizing.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/executable-guardrails.md`
- `.codex/core/closeout-loop.md`

## Legacy Path Mapping

- `_bmad-output/changes/...` -> legacy path
- `openspec/changes/...` -> preferred path for new non-trivial work

Use this copied guide only as historical context.
