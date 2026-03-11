<!-- input: repository structure changes, file responsibilities, and documentation updates -->
<!-- output: project-level documentation and maintenance rules for Codex -->
<!-- pos: shared conventions used across the .codex workflow layer -->
# Project Rules

These rules were distilled from the repo's existing `.cursor` and `.windsurf` guidance and rewritten for Codex.

## Documentation Maintenance

- If functionality, architecture, or implementation style changes, update the relevant docs before finishing.
- If a folder changes in purpose or contents, update that folder's overview doc at the same time.
- Keep documentation short and local. Prefer one small folder-level overview over a large central document.

## Folder Overviews

Each meaningful folder should have a short overview doc when practical.

Recommended format:

1. a 1-3 line summary of what the folder is for
2. a small file list with name, location, and responsibility
3. a note that the doc must be updated whenever the folder changes materially

## File Headers

When practical, non-generated files should start with concise header comments covering:

- `input`: what the file depends on
- `output`: what the file provides
- `pos`: where the file sits in the system

Also keep the header comment current when the file's responsibility changes.

Files that do not support comments or are generated artifacts can be skipped, for example:

- `package.json`
- lockfiles
- generated JSON payloads

## Workflow Preference

- Default to `Quick` for bounded coding work.
- Move to `BMM` when the change is large, unclear, or cross-cutting.
- Use `review.md`, `validate.md`, `archive.md`, and `hygiene.md` as support workflows inside the current `Quick` or `BMM` context when the task needs them.
- In `BMM`, do not stop at design prose. The change record must also define success criteria, validation gates, and the required test scope for implementation.

## Source Of Truth

- Codex should prefer `.codex/workflows/` and `.codex/core/` for execution guidance, plus `docs/system-maps/` for repo-specific hot-path context.
- `.codex/reference/` is the copied upstream reference set.
- `openspec/changes/` is the preferred location for new change records.
- If a task already uses `_bmad-output/changes/`, keep it coherent, but do not start new work there by default.
- If local execution docs and copied upstream references diverge, update the local execution docs intentionally rather than following stale copied text by accident.
