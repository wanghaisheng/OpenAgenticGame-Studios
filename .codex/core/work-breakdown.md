<!-- input: task scope, ambiguity, and expected implementation surface -->
<!-- output: a common hierarchy for breaking work into epics, features, milestones, and sub-tasks -->
<!-- pos: work breakdown rules for the repo-local harness -->
# Work Breakdown

Use this file to decide how deep a task needs to be decomposed.

## Levels

### Epic

Use for a large initiative or architecture theme that spans multiple features.

Typical shape:

- several features
- multiple milestones
- likely always `BMM`

### Feature

Use for one user-visible capability or one coherent system improvement.

Typical shape:

- one or more milestones
- may still fit in `Quick` if it compresses to a single milestone

### Milestone

This is the preferred execution unit.

Typical shape:

- one coherent delivery slice
- one validation story
- one reviewable diff
- one explicit fallback or stopping point

### Sub-task

This is the internal execution loop inside a milestone.

Typical shape:

- code -> test -> fix -> refactor
- not usually exposed as a user-facing planning layer

Do not expose sub-tasks as if they were full milestones just to make the plan look busy.

## Mode Mapping

- `Quick` usually means one milestone, with sub-tasks handled internally
- `BMM` usually means two to five milestones, each with its own validation package

Feature-level intent may appear in `BMM`, but implementation still closes milestone by milestone.

## Escalation Signals

Break work down further or escalate to `BMM` when:

- one milestone starts affecting more than one feature-level concern
- validation exceeds a comfortable local loop
- rollback or fallback is unclear
- the review scope no longer fits one screen of coherent reasoning

## Record Rule

For non-trivial `BMM` work, milestones should be tracked in the active change record under `openspec/changes/{change-name}/`.

## Strengthening Rules

- do not start implementation for non-trivial work until the current milestone is named
- do not let one milestone cover multiple unrelated behaviors just because they are all part of the same feature
- do not let milestone wording stay at roadmap level; it must be implementable and reviewable
- if a task starts in `Quick`, the milestone should usually be short enough to restate in one or two sentences
