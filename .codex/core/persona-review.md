<!-- input: completed or nearly completed changes and their validation evidence -->
<!-- output: focused review lenses for substantial work -->
<!-- pos: persona-based review prompts for the repo-local harness -->
# Persona Review

Use these lenses for substantial work, especially when the task changes shared behavior, build gates, or user-visible flows.

You do not need separate agents to use this file. A single agent can run the checks sequentially.

## Security Lens

Ask:

- did the change widen input surface, content parsing, redirects, or external calls
- did the change reduce validation, escaping, or boundary checks
- did new files or scripts introduce unsafe assumptions

## Performance Lens

Ask:

- did the change add unnecessary generation, rendering, or audit cost
- did a local fix introduce broader build or runtime overhead
- did the task increase repeated work that should stay generated or cached

## Readability Lens

Ask:

- is the change still understandable without replaying the whole branch
- are names, boundaries, and docs aligned with the new behavior
- did the task add accidental complexity or only the intended complexity

## Runtime Regression Lens

Ask:

- what user-visible path could drift even if the focused tests pass
- do routing, locale, SSR, or metadata semantics still match expectations
- does the shipped integrated path still need a broader gate

## Output Rule

If you use persona review, summarize:

- which lenses were applied
- what issues were found
- what residual risk remains after the pass

If you need a fixed summary shape, use `.codex/templates/persona-review.md`.
