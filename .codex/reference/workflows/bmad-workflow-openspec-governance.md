# OpenSpec Governance Workflow Rule

This rule makes OpenSpec the core execution policy for all agents. Any task executed by any agent MUST be managed as an OpenSpec change with complete artifacts and traceability.

## Purpose

- Enforce a single source of truth for requirements and changes
- Require planning artifacts before implementation
- Ensure every code change maps to a tracked change and task
- Provide auditable history via changes archive

## Policy (MANDATORY)

1. No ad-hoc coding. All implementation MUST be tied to an active OpenSpec change.
2. Before writing code, the agent MUST either:
   - Locate an active change in `openspec/changes/`, or
   - Create a new change following the workflow below.
3. All planning artifacts MUST be created and kept up-to-date:
   - proposal.md — intent, scope, approach
   - specs/ — delta requirements (ADDED/MODIFIED/REMOVED)
   - design.md — technical approach and decisions
   - tasks.md — implementation checklist
4. Implementation MUST follow `tasks.md` and update its checkboxes as work completes.
5. When tasks are done, the agent MUST archive the change and merge delta specs into `openspec/specs/`.
6. Validation is required before completion (lint/tests/build as applicable).

## Workflow

1) Start or Locate Change
- If a relevant change exists in `openspec/changes/`, use it.
- Otherwise, create a new folder `openspec/changes/<change-name>/` and proceed.

2) Create Artifacts
- proposal.md — capture why/what/scope
- specs/<domain>/spec.md — delta specs with ADDED/MODIFIED/REMOVED
- design.md — architecture, data flow, key decisions
- tasks.md — actionable checklist for implementation

3) Implement Tasks
- Work strictly against `tasks.md`.
- Update artifacts as you learn (proposal/specs/design/tasks).
- Keep code changes scoped to the current change.

4) Validate
- Run available quality gates (e.g., `npm run lint`, `npm test`, build).
- Fix issues before proceeding.

5) Archive & Merge
- Append/replace/remove requirements from delta into `openspec/specs/`.
- Move the finished change to `openspec/changes/archive/<date>-<change-name>/`.

## Repository Conventions

- Source of truth: `openspec/specs/`
- Active changes: `openspec/changes/<change-name>/`
- Archive: `openspec/changes/archive/<date>-<change-name>/`
- Artifact contents must reflect the actual implementation state at all times.

## Agent Integration

- This rule applies to ALL agents (dev, pm, architect, qa, etc.).
- Upon receiving a task, an agent MUST:
  1) Check for an active OpenSpec change.
  2) If absent, create one and produce artifacts.
  3) Implement only after artifacts exist and are sufficient.
  4) Keep artifacts synchronized with reality as work progresses.
  5) Validate via project commands prior to completion.
  6) Archive and merge delta specs when done.

## Acceptance Criteria

- A corresponding change exists under `openspec/changes/` (or archive when done).
- proposal/design/tasks are complete and consistent.
- Delta specs accurately describe changes and are merged to `openspec/specs/` on archive.
- Quality gates pass (lint/tests/build).

## References

- Getting Started with OpenSpec: `docs/openspec-getting-started.md`

## Usage

- Reference this policy as the default workflow for any agent.
- If a task request does not map to an existing change, immediately start a new one and proceed per this rule.
