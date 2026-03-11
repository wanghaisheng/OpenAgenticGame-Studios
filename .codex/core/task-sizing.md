<!-- input: task scope, acceptance clarity, touched systems, and expected diff size -->
<!-- output: sizing guidance for staying in Quick or escalating to BMM -->
<!-- pos: shared task-sizing rules for the repo-local Codex layer -->
# Task Sizing

Use this to decide whether work can stay in `Quick` or must move to `BMM`.

## Target Milestone Shape

Aim for one milestone that:

- changes one coherent behavior, pipeline, or contract surface
- fits roughly within 300 to 800 net changed lines
- touches roughly 3 to 12 files
- can be validated locally in about 10 to 20 minutes
- can be reviewed without scrolling through unrelated subproblems

Treat this as the preferred execution envelope, not as optional flavor text.

## Stay In Quick When

Quick is appropriate when all of these are mostly true:

- the request can be stated clearly in one or two sentences
- acceptance criteria are already known
- the work targets one primary behavior or one bounded pipeline
- no new shared contract, migration, or rollout plan is needed
- the diff still fits the milestone shape above

## Escalate To BMM When

Move to `BMM` when any of these are true:

- requirements are unclear or competing interpretations exist
- the task crosses multiple subsystems, such as routing plus content generation plus SEO auditing
- the change introduces a new shared contract, generator behavior, architecture rule, or release gate
- the work needs milestone sequencing, rollout planning, or explicit non-goals
- the diff keeps expanding beyond the Quick envelope

## Split Patterns

Use one of these patterns instead of letting a task sprawl:

- analysis -> shim -> migrate -> remove old path
- spec -> implement -> audit -> archive
- generator change -> snapshot regen -> runtime verify
- SEO change -> head verify -> audit verify -> integrated build gate

## Decomposition Rules

Before implementation:

1. state the primary behavior, pipeline, or contract surface
2. state the milestone boundary
3. state the dominant validation story
4. state the stopping point if later milestones never ship

If those four statements are fuzzy, the task is not ready to implement.

## Edge Cases

- pure docs or configuration tasks can be smaller, but they still need a coherent closeout
- exploratory work should become a bounded spike, then either close or escalate to BMM
- large refactors should be broken into reversible milestones, not one branch-sized rewrite

## Mid-Task Escalation

If a task starts in `Quick` and then grows:

1. stop treating it as a simple scoped implementation
2. open or update `openspec/changes/{change-name}/`
3. decompose the remaining work into milestones
4. continue in `BMM` without discarding the work already done
