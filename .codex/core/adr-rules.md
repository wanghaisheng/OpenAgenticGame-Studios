<!-- input: architecture-impacting changes, change records, and durable system decisions -->
<!-- output: rules for recording architecture and durable workflow decisions -->
<!-- pos: ADR handling guidance for the repo-local harness -->
# ADR Rules

This repository does not currently keep a dedicated `docs/ADR/` tree.

Use the active change record as the first ADR surface, then sync durable outcomes into the relevant technical docs.

## Create Or Update A Decision Record When

- system boundaries or architecture change
- a new shared contract or generator rule is introduced
- a build gate, audit gate, or validation standard changes
- a compatibility shim is added or removed
- Quick or BMM behavior changes in a way future tasks must inherit

## Where To Record It

Primary:

- `openspec/changes/{change-name}/design.md`

Durable follow-through when the decision affects the long-term system:

- `docs/technical/project-architecture-overview.md`
- another relevant doc under `docs/technical/`
- `.codex/` workflow docs when the decision changes agent behavior

## Minimum Decision Content

Record:

- context
- decision
- tradeoffs
- validation impact
- migration or follow-up implications

## Rule

If a future engineer would need this decision to avoid repeating the same debate, it should be recorded.
