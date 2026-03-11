<!-- input: validated changes, change records, and final implementation state -->
<!-- output: a closed-out task with durable notes for later maintenance -->
<!-- pos: archive workflow for the local Codex layer -->
# Archive Workflow

Use this when a change is complete and should leave behind a clean record.

## Archive Steps

1. Confirm the implementation is done or explicitly paused.
2. Update the active change record under `openspec/changes/{change-name}/` when one exists.
3. If the task is still using a legacy `_bmad-output/changes/{change-name}/` folder, keep it internally consistent and note that it is legacy.
4. Record any follow-up items that were intentionally deferred.
5. Make sure local docs point to final behavior, not in-progress plans.
6. Leave enough context that a later engineer can understand what happened without replaying the whole task.

## Good Archive Output

A good closeout note captures:

- final scope
- verification performed
- known limitations
- next step, if any
