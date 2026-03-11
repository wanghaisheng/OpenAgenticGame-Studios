<!-- input: active tasks, internal harness docs, and copied upstream references -->
<!-- output: a compact index of the repo-local Codex workflows -->
<!-- pos: workflow directory index for the local Codex layer -->
# Workflow Index

## Primary Modes

- `router.md`: choose between `Quick` and `BMM`.
- `quick.md`: scoped implementation mode for clear, bounded work.
- `bmm.md`: full requirement-to-implementation mode for larger or unclear work.

## Support Workflows

- `review.md`: findings-first review pass for an existing diff or branch.
- `validate.md`: readiness gate before closing meaningful work.
- `archive.md`: close out a completed change and leave a durable record behind.
- `hygiene.md`: bounded cleanup and debt-reduction workflow for existing repo drift.

## Compatibility Aliases

- `dev.md`: compatibility alias that now routes to `quick.md`.
- `spec.md`: compatibility alias that now routes to `bmm.md`.

## How To Use

For most requests:

1. start with `router.md`
2. follow either `quick.md` or `bmm.md`
3. use `review.md`, `validate.md`, `archive.md`, or `hygiene.md` only when the task specifically calls for them

## Internal Shared Docs

Both primary modes automatically rely on:

- `../core/harness.md`
- `../core/task-sizing.md`
- `../core/milestone-design.md`
- `../core/work-breakdown.md`
- `../core/validation-matrix.md`
- `../core/closeout-loop.md`
- `../core/executable-guardrails.md`
- `../core/persona-review.md`
- `../core/adr-rules.md`
- `../core/observability.md`
- `../core/openspec-sync.md`
- `../core/maturity-checklist.md`

Useful scaffolds:

- `../templates/quick-prompt.md`
- `../templates/bmm-spec-checklist.md`
- `../templates/milestone.md`
- `../templates/milestone-status.md`
- `../templates/persona-review.md`
- `../templates/closeout.md`

For repo-specific context, use:

- `../../docs/system-maps/runtime.md`
- `../../docs/system-maps/content-pipeline.md`
- `../../docs/system-maps/seo-audit.md`
