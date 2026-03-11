<!-- input: repo-local workflows, internal harness docs, and upstream reference copies -->
<!-- output: the primary Codex workflow entrypoint for this repository -->
<!-- pos: main index for the repo-local Codex layer -->
# Codex Development Layer

This folder is the Codex workflow layer for this repository.

User-facing mode selection stays intentionally small:

- `Quick`: scoped implementation, bug fixes, and bounded refactors
- `BMM`: requirement discovery through implementation for larger or unclear work

Harness, task sizing, milestone design, and validation gates live in `.codex/`; repo-specific system maps live in `docs/system-maps/`. They are all support docs loaded by the two modes, not separate user modes.

## Start Here

1. Read `.codex/workflows/router.md`.
2. Enter either `.codex/workflows/quick.md` or `.codex/workflows/bmm.md`.
3. Use `.codex/workflows/review.md`, `.codex/workflows/validate.md`, `.codex/workflows/archive.md`, and `.codex/workflows/hygiene.md` as support workflows when the task needs them.
4. Open `.codex/reference/` only when the lightweight local workflow docs are not enough.
5. For any non-trivial task, enforce decomposition through `.codex/core/work-breakdown.md`, `.codex/core/task-sizing.md`, and `.codex/core/milestone-design.md` before implementation grows.
6. Load repo-specific hot-path maps from `docs/system-maps/` when the active workflow calls for them.

## Folder Map

- `workflows/`: primary execution docs. Only `quick.md` and `bmm.md` are user-facing modes.
- `core/`: internal harness rules, task and milestone decomposition rules, hard gates, review lenses, ADR rules, observability guidance, and openspec sync rules shared by both modes.
- `templates/`: reusable prompt and closeout scaffolds for Quick and BMM work.
- `reference/`: copied upstream BMAD/OpenSpec material kept for local reference and compatibility.
- `LESSONS-LEARNED.md`: recurring project mistakes and local implementation lessons.
- `quick-dev.png` and `bmm-dev.png`: copied diagrams from the upstream workflow set.

Outside `.codex/`:

- `docs/system-maps/`: repo-specific system maps for high-frequency change areas. These stay outside `.codex/` because they are coupled to the current project codebase.

## Modes

### Quick

Use Quick when:

- the task is a bug fix, scoped feature, or bounded refactor
- acceptance criteria are already clear
- the touched surface area is limited
- existing tests or straightforward local checks can verify the result
- the work still fits one coherent milestone

Primary docs:

- `.codex/workflows/router.md`
- `.codex/workflows/quick.md`
- `.codex/workflows/review.md`
- `.codex/workflows/validate.md`

### BMM

Use BMM when:

- requirements are unclear or still need discovery
- the change is architectural, cross-cutting, or high-risk
- the work should leave behind a reusable change record
- the task needs proposal, design, task breakdown, and implementation
- the work needs more than one milestone

Primary docs:

- `.codex/workflows/router.md`
- `.codex/workflows/bmm.md`
- `.codex/workflows/validate.md`
- `.codex/workflows/archive.md`

## Change Record Convention

For new non-trivial changes, prefer:

`openspec/changes/{change-name}/`

Use `kebab-case` for `{change-name}`.

If a task already has a coherent legacy change folder under `_bmad-output/changes/{change-name}/`, keep that record consistent instead of migrating it mid-task. New change records should start in `openspec/changes/`.

## Strengthening Rule

In this repository, stronger workflow means:

- every non-trivial task must be decomposed before implementation expands
- every implementation task must map to one reviewable milestone
- `dev.md` and `spec.md` are compatibility aliases only and inherit the same decomposition and loop rules as `quick.md` and `bmm.md`
- milestone status, validation evidence, and residual risk must be visible in the active record before closeout

## Sync Policy

This folder is a repo-local workflow layer built on top of copied upstream BMAD/OpenSpec references.

When the workflow changes:

1. update the local execution docs under `.codex/workflows/` and `.codex/core/`, plus repo-specific maps under `docs/system-maps/`
2. keep `AGENTS.md` aligned with the current preferred user-facing flow
3. refresh `.codex/reference/` only when upstream source material actually changes
