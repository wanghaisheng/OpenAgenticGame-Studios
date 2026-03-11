<!-- input: finished implementation, validation evidence, and doc updates -->
<!-- output: a consistent final self-check before closing work -->
<!-- pos: shared closeout loop for Quick and BMM -->
# Closeout Loop

Before closing a task, run this loop.

If you want a ready-made summary shape, use `.codex/templates/closeout.md`.

## Ralph Loop

1. Re-read the user request and confirm the final diff still matches it.
2. Run the selected validation package and required hard gates.
3. Self-review against `harness.md`, the active mode expectations, and the current milestone boundary.
4. If a command fails, read the output, report, or latest log before changing code.
5. Fix the actual cause, then re-run the affected validation.
6. Update milestone status, changed docs, and any ADR follow-up that the task created.
7. Only close when the implementation, validation, and documentation story is coherent.

## Closeout Checklist

Capture all of these:

- what changed
- which milestone closed
- what was verified
- what could not be verified locally
- what remains risky or deferred
- which docs or change records were updated

## Closure Standard

Do not close work on a vague statement like "should be fine".

Close only when:

- required validations are green or clearly explained
- docs and change records match the implementation
- residual risk is explicit rather than implied
