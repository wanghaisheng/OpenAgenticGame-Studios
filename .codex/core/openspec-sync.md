<!-- input: active change records, milestone plans, and implementation progress -->
<!-- output: rules for keeping .codex milestone design aligned with openspec change records -->
<!-- pos: sync rules between the repo-local harness and openspec -->
# OpenSpec Sync

Use this file when work is tracked under `openspec/changes/{change-name}/`.

The goal is to keep milestone design in `.codex` aligned with the change record, without forcing a second planning system.

## Minimum Sync Rules

- `README.md` should summarize current scope, validation evidence, and known limitations
- `tasks.md` should reflect milestone-level progress, not only a flat unchecked wish list
- `design.md` should record durable architecture or workflow decisions when they matter

## Milestone Sync Rule

For non-trivial BMM work:

- each milestone should appear in `tasks.md` as a grouped section or clearly related checklist block
- milestone status may also be summarized in `README.md` when progress needs a current snapshot
- use `.codex/templates/milestone-status.md` when progress is complex enough to need explicit status tracking

## Update Triggers

Update the active change record when:

- milestone scope changes
- validation scope changes
- a milestone completes or is blocked
- a fallback or compatibility approach changes
- residual risk changes materially

## One-Truth Rule

Do not track milestone truth in three different places.

If the task uses an `openspec` change record, the durable progress state should live there, with `.codex` providing the rules and templates.
