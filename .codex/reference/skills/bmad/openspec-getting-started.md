<!-- input: upstream OpenSpec getting-started guidance and the repo-local BMAD workflow model -->
<!-- output: a compatibility note for readers opening the copied OpenSpec skill guide -->
<!-- pos: reference-layer OpenSpec getting-started skill compatibility guide -->
# OpenSpec Getting Started Skill Compatibility Guide

This copied getting-started guide is retained for upstream OpenSpec background.

For the shared terminology and path translation table, use `.codex/reference/LEGACY-MAPPING.md`.

In this repository, the active local flow is:

- route through `.codex/workflows/router.md`
- choose `.codex/workflows/quick.md` or `.codex/workflows/bmm.md`
- keep change records in `openspec/changes/<change-name>/` for new non-trivial work

## Local Rules Added On Top

The local workflow adds repo-specific control layers:

- harness rules: `.codex/core/harness.md`
- milestone design: `.codex/core/milestone-design.md`
- work breakdown: `.codex/core/work-breakdown.md`
- openspec sync: `.codex/core/openspec-sync.md`
- closeout and hard gates: `.codex/core/closeout-loop.md` and `.codex/core/executable-guardrails.md`

## Legacy Mapping

- `Quick Dev` -> local `Quick`
- `_bmad-output/changes/...` -> legacy path
- `_bmad/...` -> copied upstream asset path

Use this copied guide for general OpenSpec concepts, not as the authoritative local execution guide.
