<!-- input: recurring implementation mistakes, repo-specific hot paths, and recent delivery incidents -->
<!-- output: compact lessons that should influence future Quick and BMM work -->
<!-- pos: repo-local lessons learned for Codex execution -->
# Lessons Learned

Use these lessons when working in this repository.

## 1. Treat Generated Pipelines As Real Product Surface

- Changes to content, routes, sitemap inputs, prerender inputs, or snapshots often require generator validation, not just code review.
- Prefer `npm run prebuild` or the relevant generator commands before assuming a change is isolated.
- If generated output affects runtime or audits, finish with `npm run build:dev`.

## 2. SSR Head And SEO Behavior Need Explicit Proof

- Metadata changes are easy to get partially right and still ship broken output.
- Use `npx vitest run tests/ssr-head.test.ts` plus the SEO audit scripts when head behavior changes.
- Do not assume audit failures are caused by the current change until the report is inspected.

## 3. I18n And Navigation Changes Can Have History-Semantics Regressions

- Locale and language-entry behavior is not just text replacement; history behavior and SSR output matter too.
- Run targeted i18n tests when touching language detection, switching, or prompt flows.
- Use `npm run build:dev` when locale behavior changes feed routing or SSR.

## 4. Audit Failures Must Be Attributed Before Fixing

- `build:dev` includes post-build and audit stages, so a non-zero exit can come from late-stage checks rather than the new code path itself.
- Read the failing report or tail symptom first.
- Distinguish between a new regression and an existing repository-level warning or gate failure.

## 5. Keep One Change Record Truth Source

- New non-trivial work should start under `openspec/changes/{change-name}/`.
- If a task already lives under `_bmad-output/changes/{change-name}/`, keep it coherent rather than splitting records mid-task.
- A weak or drifting change record causes BMM work to lose continuity faster than code changes do.

## 6. Reference Docs Are Not The Runtime Workflow

- `.codex/reference/` is useful background, but it should not override the repo-local execution docs.
- The active workflow lives in `.codex/workflows/` and `.codex/core/`; repo-specific hot-path maps now live in `docs/system-maps/`.
- If a reference file says something different, treat it as upstream context until the local docs are intentionally updated.
