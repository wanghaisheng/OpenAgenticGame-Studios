<!-- input: a larger or unclear request and intended change record -->
<!-- output: a reusable BMM change-record scaffold -->
<!-- pos: planning scaffold for repo-local BMM work -->
# BMM Change-Record Template

Use this scaffold when a task should go through BMM and should leave behind a full change record under `openspec/changes/<change-name>/`.

The goal is not to produce a vague spec. The goal is to produce a change record that is ready for milestone-by-milestone implementation under the repo-local harness.

## Output Expectation

Generate or update this structure:

- `openspec/changes/<change-name>/README.md`
- `openspec/changes/<change-name>/proposal.md`
- `openspec/changes/<change-name>/design.md`
- `openspec/changes/<change-name>/tasks.md`
- `openspec/changes/<change-name>/specs/<area>/spec.md` when the task introduces or changes a durable contract

## Required Workflow Alignment

The generated change record must align with:

- `.codex/core/work-breakdown.md`
- `.codex/core/task-sizing.md`
- `.codex/core/milestone-design.md`
- `.codex/core/validation-matrix.md`
- `.codex/core/adr-rules.md`
- `.codex/core/persona-review.md`
- `.codex/core/closeout-loop.md`

That means:

- decompose the work into milestone-level execution slices
- keep each milestone bounded and reviewable
- define validation by package, not only by ad hoc command lists
- add ADR-grade content when the change affects durable rules or shared behavior
- make closeout expectations explicit in `tasks.md`

## Prompt Scaffold

```text
Route this through BMM.

Task:
<what needs to change>

Change name:
<kebab-case change name>

Problem:
<what is wrong, missing, risky, or unclear today>

Why now:
<why this should be addressed now rather than deferred>

Scope:
- in scope: <items>
- out of scope: <items>

Affected systems:
- <runtime | content-pipeline | seo-audit | i18n | build | docs | other>

Required outputs:
- create or update `openspec/changes/<change-name>/README.md`
- create or update `openspec/changes/<change-name>/proposal.md`
- create or update `openspec/changes/<change-name>/design.md`
- create or update `openspec/changes/<change-name>/tasks.md`
- create or update `openspec/changes/<change-name>/specs/<area>/spec.md` if the work changes a durable contract

Execution rules:
- use `.codex/core/work-breakdown.md` and `.codex/core/task-sizing.md`
- decompose the work into feature intent plus milestone execution slices
- design each milestone using `.codex/core/milestone-design.md`
- choose validation using `.codex/core/validation-matrix.md`
- use `.codex/core/adr-rules.md` when the change introduces durable decisions
- require persona review when milestones change shared or user-visible behavior
- keep milestone status, validation evidence, and residual risk explicit

Acceptance criteria:
- <criterion 1>
- <criterion 2>

Success criteria:
- <criterion 1>
- <criterion 2>
```

## File Structure Requirements

### `README.md`

Use this shape:

```text
# <Change Title>

## Status
- planned | in_progress | validated | archived

## Harness Alignment
- name the relevant `.codex/core` docs this change must follow
- state whether this is Quick-sized or BMM-sized work

## Source Context
- source docs, datasets, incidents, or existing change records

## Why This Change Exists
- concise summary of the problem and current gap

## Relationship To Existing Changes
- link to adjacent change records or local docs

## Execution Model
- explain whether implementation will happen milestone by milestone
- note any special rollout, migration, or review rule

## Validation Strategy
- map the work to validation packages from `validation-matrix.md`

## Milestone Shape
1. <milestone 1>
2. <milestone 2>
3. <milestone 3>
```

### `proposal.md`

Use this shape:

```text
# Proposal: <Change Title>

## Intent
- what this change is meant to accomplish

## Why This Change
- why the change is needed now

## In Scope
- bounded list

## Out Of Scope
- bounded list

## Acceptance Criteria
1. <criterion>
2. <criterion>

## Success Criteria
- outcome-oriented measures, not just file creation
```

### `design.md`

Use this shape:

```text
# Design: <Change Title>

## Problem Statement
- concise problem framing

## ADR 1: <short decision title>
Context:
- <context>
Decision:
- <decision>
Tradeoffs:
- <tradeoff>
Validation impact:
- <impact>
Migration and follow-up implications:
- <follow-up>

## ADR 2: <optional second decision>
...

## Milestone Sizing Note
- restate the preferred execution unit for this change

## Milestone N: <name>
Goal:
- <one coherent outcome>

Execution slices:
- <item>
- <item>

Out of scope:
- <item>
- <item>

Touched systems:
- <runtime | content-pipeline | seo-audit | other>

Entry context:
- <docs, maps, specs that must be read first>

Acceptance criteria:
- <criterion>
- <criterion>

Validation package:
- <package from validation-matrix.md>
- <extra gate if needed>

Persona review:
- <required lens or none>

Fallback note:
- <pause point, rollback, or compatibility note>

Next dependency:
- <next milestone or none>
```

### `tasks.md`

Use this shape:

```text
# Tasks

## Progress Snapshot
- source inputs and current state

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

## M1. <milestone title>
- [ ] M1.1 <task>
- [ ] M1.2 <task>

## M2. <milestone title>
- [ ] M2.1 <task>
- [ ] M2.2 <task>

## Closeout Rule
- selected validation package
- commands that ran
- pass or fail status
- residual risk
- ADR or doc follow-up required
```

### `specs/<area>/spec.md`

Create this when the change modifies a durable contract, rule, or behavior standard.

Use this shape:

```text
# <Area> Spec

## Requirements

### R1. <requirement>
Acceptance:
- <criterion>
- <criterion>

### R2. <requirement>
Acceptance:
- <criterion>
- <criterion>

## Non-Requirements
- <explicitly excluded items>

## Validation Notes
- required package from `validation-matrix.md`
- closeout evidence expected for implementation
```

## Quality Bar

The generated BMM change record is not complete if it does any of these:

- leaves milestones at roadmap level instead of implementation level
- lists raw commands without naming the validation package
- omits ADR content for durable shared decisions
- omits persona review expectations for substantial milestones
- omits the closeout rule or milestone execution loop
- turns the task list into a flat backlog with no milestone grouping
