<!-- input: failing commands, generated reports, temp logs, and audit output -->
<!-- output: guidance for diagnosing failures before changing code -->
<!-- pos: observability guidance for the repo-local harness -->
# Observability

Use this file when a command, build, or audit fails.

The goal is to diagnose before patching.

## Evidence Sources

Use these in roughly this order:

1. command stderr or tail output
2. the latest report under `reports/`
3. root-level temp logs such as `.codex-tmp-*.log`
4. the active `openspec/changes/{change-name}/` notes when the failure conflicts with planned behavior

## Diagnosis Order

1. identify the first failing command, not just the last umbrella command
2. read the latest report or log for that failing stage
3. decide whether the issue is:
   - caused by the current change
   - an exposed pre-existing failure
   - a flaky or environmental problem
4. only then choose a fix or explicit risk callout

## Common Repo Patterns

### `npm run build:dev`

Typical failure order to inspect:

1. `prebuild` generators
2. client or server build output
3. post-build scripts
4. link or head audits
5. SEO coverage check

Do not assume the final non-zero exit came from the first code path you changed.

### SEO And Audit Failures

- read the newest file in `reports/`
- compare the failing symptom with the touched route or locale area
- decide whether the audit found a new regression or an older repository-wide gap

### Generator Failures

- find the first broken generator command
- fix the upstream content or generator issue there
- avoid patching only the final generated artifact

## Pre-Existing Failure Rule

You can treat a failure as pre-existing only when at least one of these is true:

- the same failure already exists in the latest report before your change
- the failing area is outside the touched systems and unchanged by the current diff
- the change record or prior notes already list it as unresolved debt

If that is still uncertain, do not present it as definitively pre-existing.

## Rule

Do not make speculative edits when the failure evidence has not been read.
