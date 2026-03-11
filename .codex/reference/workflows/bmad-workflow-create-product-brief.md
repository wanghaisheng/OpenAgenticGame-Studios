<!-- input: copied product-brief wrapper and the repo-local BMM workflow model -->
<!-- output: a compatibility note for the copied product-brief workflow -->
<!-- pos: reference-layer product-brief compatibility guide -->
# Product Brief Compatibility Guide

This copied wrapper is kept for upstream background only.

There is no separate user-facing `product brief` mode in this repository.

## Local Equivalent

Product discovery and brief-style work now routes through:

- `.codex/workflows/bmm.md`
- `.codex/core/work-breakdown.md`
- `.codex/core/milestone-design.md`
- `.codex/core/openspec-sync.md`

## Local Mapping

- older `create-product-brief` language maps into the discovery portion of local `BMM`
- `_bmad-output/...` references are legacy only

Use this copied guide only when you need upstream BMM context beyond the local BMM docs.
