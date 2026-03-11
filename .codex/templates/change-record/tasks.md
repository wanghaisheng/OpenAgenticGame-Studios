<!-- input: a new or updated BMM change record -->
<!-- output: starter tasks scaffold for openspec/changes/<change-name>/tasks.md -->
<!-- pos: starter tasks template -->
# Tasks

## Progress Snapshot

- <source inputs>
- <current state>

## Milestone Execution Loop

1. read the active change and relevant `.codex/core` docs
2. confirm the milestone still fits the sizing rule
3. implement one bounded milestone only
4. select the validation package from `validation-matrix.md`
5. run commands, inspect first failure, fix, and repeat
6. self-review against the active change and spec
7. apply persona review when required
8. update ADR content when durable decisions change
9. record what ran, what passed, and what remains unverified

## M1. <Milestone Title>

- [ ] M1.1 <task>
- [ ] M1.2 <task>

## M2. <Milestone Title>

- [ ] M2.1 <task>
- [ ] M2.2 <task>

## Closeout Rule

- selected validation package
- commands that ran
- pass or fail status
- residual risk
- ADR or doc follow-up required
