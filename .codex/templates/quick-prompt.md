<!-- input: a clear scoped request, touched files, and expected validation -->
<!-- output: a reusable Quick-mode prompt scaffold -->
<!-- pos: prompt scaffold for repo-local Quick work -->
# Quick Prompt Template

Use this scaffold when you want a compact Quick request that still carries the right constraints.

```text
Route this through Quick.

Task:
<one or two sentence request>

Context:
- touched area: <runtime | content-pipeline | seo-audit | other>
- expected files: <optional>
- acceptance criteria: <clear desired outcome>

Constraints:
- inspect the local code path before editing
- compress the work into one coherent milestone before implementation
- keep the diff bounded to that milestone
- use the repo-local validation matrix
- use the repo-local closeout loop
- update affected docs before closing

Validation:
- run <targeted command 1>
- run <targeted command 2>
- run `npm run build:dev` if the change touches shipped runtime, SSR, SEO, or generated output

Closeout:
- report the milestone that closed
- report what was verified, what was not verified, and residual risk
```
