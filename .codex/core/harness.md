<!-- input: routed task mode, repo conventions, system maps, and repo-level guardrails -->
<!-- output: shared execution constraints applied under Quick and BMM -->
<!-- pos: internal harness rules for the repo-local Codex layer -->
# Harness

This is the internal execution constitution shared by `Quick` and `BMM`.

It exists to make the workflow stronger without making the user learn more modes.

## Non-Negotiable Rules

- Users only choose between `Quick` and `BMM`.
- Always inspect local code and docs before proposing or editing changes.
- Prefer repo-local workflow docs over copied upstream reference docs.
- Prefer `openspec/changes/` for new change records.
- Do not leave validation, risk, or documentation sync as implicit cleanup.
- Treat `.codex/reference/` as background material, not the active execution layer.

## Forbidden

- Do not close work without running the required validation package.
- Do not silently ignore a failing command, audit, or report.
- Do not keep a task in `Quick` once it clearly exceeds the sizing envelope.
- Do not edit generated output instead of the source generator or source content.
- Do not create new non-trivial change records under `_bmad-output/changes/`.
- Do not let docs, change records, and implementation drift apart at closeout.

## Musts

- Every meaningful change must name the touched system area and load the relevant repo map.
- Every non-trivial task must be decomposed before implementation expands.
- Every implementation task must map to one named milestone, even in `Quick`.
- Every meaningful change must choose a validation package from `validation-matrix.md`.
- Every meaningful change must finish with the closeout loop from `closeout-loop.md`.
- Substantial work must include a persona review pass from `persona-review.md`.
- Architecture, contract, or durable system-rule changes must follow `adr-rules.md`.
- Failures must be diagnosed using `observability.md` before broad speculative fixes.

## Dependency Rules

Use these direction rules when changes cross system boundaries:

- runtime routes and entrypoints may depend on route helpers, SEO helpers, and generated artifacts
- generator and audit scripts may shape runtime behavior, but runtime code should not patch generator outputs by hand
- locale SEO files feed runtime metadata and audits, so SEO changes need both runtime and audit proof
- change records describe the work; they do not replace runnable validation

## Naming And Record Rules

- use `kebab-case` for `openspec/changes/{change-name}/`
- keep one primary truth source per task
- if a task already uses `_bmad-output/changes/{change-name}/`, keep it coherent but treat it as legacy
- update local docs when folder responsibility, behavior, or workflow expectations change

## ADR Trigger Rules

Read `adr-rules.md` and leave a durable decision record when the change:

- changes architecture or system boundaries
- introduces a new shared contract, generator rule, or build gate
- changes how Quick or BMM should operate
- adds a compatibility shim or removes an old compatibility path

## Standard Loop

1. Route the task through `workflows/router.md`.
2. Load the relevant system map for the touched area.
3. Inspect the existing code and documentation.
4. Check `task-sizing.md` before implementation expands.
5. Decompose the work using `work-breakdown.md` and `milestone-design.md`.
6. Execute the chosen mode one milestone at a time.
7. Apply the required validation package and hard gates.
8. Run persona review when the change is substantial.
9. Sync docs and change-record state.
10. Close with verified scope, unverified gaps, residual risk, and milestone status.
