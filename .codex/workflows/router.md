<!-- input: task size, uncertainty, review intent, and existing change artifacts -->
<!-- output: workflow selection guidance for Codex -->
<!-- pos: workflow router for the local Codex layer -->
# Router

Use this document to choose the next workflow.

## Route To `quick.md`

Choose Quick when all of these are effectively true:

- the task is a bug fix, scoped feature, or bounded refactor
- acceptance criteria are already clear
- the touched surface area is limited
- verification can be handled with focused local checks
- the work still fits one coherent milestone

Quick automatically pulls in the internal harness, decomposition, validation, and closeout docs.

## Route To `bmm.md`

Choose BMM when any of these are true:

- requirements are unclear or need discovery
- the change affects architecture, shared contracts, or multiple subsystems
- the user asks for planning, design, proposal, or spec work
- the task should leave behind a reusable change record
- the work is likely to exceed the Quick sizing envelope
- the work needs more than one milestone or its milestone boundary is unclear

BMM still uses the same internal harness, but adds change-record discipline and milestone planning.

## Use Support Workflows As Needed

- `review.md`: when the user explicitly asks for a review, or when a final findings-first pass is needed
- `validate.md`: when implementation is mostly done and needs a closing gate
- `archive.md`: when the task is complete and should leave behind final notes

These are support workflows, not separate user-facing modes.

## Decomposition Rule

Before doing substantial work:

1. identify the primary behavior or contract surface
2. decide whether it fits one milestone
3. if not, route to `bmm.md` and write the milestones down

## Fast Heuristic

- Small and clear and one milestone: `quick.md`
- Large or unclear or multi-milestone: `bmm.md`
- Review requested: `review.md` inside the current mode context
- Closing work: `validate.md`, then `archive.md` if a durable record is needed
