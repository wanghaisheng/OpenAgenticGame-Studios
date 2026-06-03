# Codex Migration Guide

OpenAgenticGame Studios now uses OpenAI Codex as its native agentic coding environment. The previous Claude Code-specific `.claude/` integration has been removed in favor of a portable Codex-first setup.

## What changed

| Area | Previous | Current |
| --- | --- | --- |
| Primary agent instructions | `CLAUDE.md` / `.claude/` | `AGENTS.md` |
| Workflow layer | Claude Code hooks and settings | `.codex/workflows/` + `.codex/core/` |
| Skills | `.claude/skills/<name>/SKILL.md` | `refenrece/skills/<name>/SKILL.md` |
| Rules | `.claude/rules/*.md` | `refenrece/rules/*.md` |
| Templates | `.claude/docs/templates/*.md` | `refenrece/docs/templates/*.md` |
| Session automation | Claude Code hook scripts | Codex workflow routing and validation gates |

## Codex quick start

```bash
npm install -g @openai/codex
codex --login
codex
```

From the repository root, ask Codex to read `AGENTS.md` and `.codex/README.md` before starting work.

## Recommended flow

1. Route the task through `.codex/workflows/router.md`.
2. Use `.codex/workflows/quick.md` for scoped implementation.
3. Use `.codex/workflows/bmm.md` for larger or unclear work that needs discovery, milestones, and durable records.
4. Validate with `.codex/workflows/validate.md` before closeout.
5. Archive reusable learnings through `.codex/workflows/archive.md` when the workflow calls for it.

## Legacy compatibility

The universal reference system in `refenrece/` remains AI-agnostic. Cursor, Windsurf, Claude Code, and future tools can still read those references, but Codex is now the default supported runtime for this repository.
