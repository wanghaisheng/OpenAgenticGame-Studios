<!-- input: diff, changed files, tests, and expected behavior -->
<!-- output: findings-first review output with concrete risks and gaps -->
<!-- pos: code review workflow for Codex in this repository -->
# Review Workflow

Use this whenever the task is a review or when you want a final risk pass.

This is a support workflow inside `Quick` or `BMM`, not a separate user-facing mode.

## Review Standard

Findings come first.

Order them by severity and include:

- the issue
- why it matters
- where it is, with file and line references when available
- what is missing or likely to regress

## Priorities

Focus on:

- correctness bugs
- regressions
- broken assumptions
- missing or weak tests
- data integrity and state issues
- performance problems that materially affect behavior

## Output Format

1. Findings
2. Open questions or assumptions
3. Brief change summary only if needed

If no findings are discovered, say so explicitly and still mention residual risk or missing verification.

## Upstream Reference

For the full source workflow, see:

- `.codex/reference/workflows/@review.md`
- `.codex/reference/workflows/bmad-workflow-code-review.md`
