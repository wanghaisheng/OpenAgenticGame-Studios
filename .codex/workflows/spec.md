<!-- input: legacy spec prompts, repository context, and change-planning tasks -->
<!-- output: compatibility routing for the BMM workflow -->
<!-- pos: compatibility alias for the BMM workflow -->
# Spec Workflow

This file remains for compatibility with older `@spec` or spec-first prompts.

In this repository, spec-led work now lives in:

- `.codex/workflows/bmm.md`

## What To Do

1. Follow `bmm.md` as the primary workflow.
2. Apply the shared internal rules from:
   - `.codex/core/harness.md`
   - `.codex/core/work-breakdown.md`
   - `.codex/core/task-sizing.md`
   - `.codex/core/milestone-design.md`
   - `.codex/core/validation-matrix.md`
   - `.codex/core/closeout-loop.md`
   - `.codex/core/adr-rules.md`
   - `.codex/core/openspec-sync.md`
3. Prefer new change records under `openspec/changes/{change-name}/`.
4. If the task already has a coherent legacy folder under `_bmad-output/changes/{change-name}/`, keep that record accurate rather than splitting the truth source mid-task.
5. Decompose the work into milestone-level execution slices instead of leaving the spec as one large planning block.
6. Keep milestone validation, ADR, and closeout expectations explicit in the change record.

## Compatibility Rule

Keep treating `spec.md` as an alias, not a separate user-facing mode. It inherits the same milestone-design, ADR, validation, and closeout rules as `bmm.md`.
