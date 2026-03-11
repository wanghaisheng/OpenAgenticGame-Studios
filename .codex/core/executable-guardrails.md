<!-- input: task type, touched systems, and repo-level command gates -->
<!-- output: hard command-based guardrails that must be satisfied before closeout -->
<!-- pos: executable validation and release guardrails for the repo-local harness -->
# Executable Guardrails

These are hard gates, not soft advice.

A task is not ready to close if a required guardrail was skipped or is red.

## Baseline Guardrails

Run these when the task changes code:

- `npm run check:syntax`
- `npm run lint` when the touched files are covered by the lint surface
- targeted tests from `validation-matrix.md`

## Integration Guardrails

These become mandatory when the touched area demands them:

- `npm run build:dev` for cross-system, SSR, SEO, routing, or generated-output changes
- `node scripts/run-check-links.mjs --mode=dev` for SEO or audit-facing changes
- `node scripts/seo/check-seo-coverage.js` for locale SEO and coverage changes
- `npm run i18n:check` for i18n or translated-output changes
- `npm run prebuild` when multiple generation steps are directly affected

## Skip Rule

Do not skip a required guardrail just because a narrower test passed.

If the shipped behavior depends on an integrated path, the integrated path must run.

## Failure Rule

When a guardrail fails:

1. inspect the first failing command or latest relevant report
2. decide whether the failure is caused by the current change or is pre-existing
3. either fix it or carry it forward explicitly as a known gap

## Evidence Rule

At closeout, name the commands that were used as proof.

Do not summarize with vague phrases like "validated locally" without the command package.
