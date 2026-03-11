<!-- input: active milestone progress, validation state, and remaining blockers -->
<!-- output: a reusable milestone tracking scaffold -->
<!-- pos: milestone status scaffold for repo-local BMM work -->
# Milestone Status Template

Use this scaffold to track milestone state in an active change record.

```text
Milestone:
<name>

Status:
- planned | in_progress | blocked | validated | archived

Goal:
- <one-line milestone outcome>

Current summary:
- <one-line state summary>

Completed:
- <done item>

Remaining:
- <remaining item>

Validation evidence:
- <command and result>

Persona review:
- lenses applied: <security | performance | readability | runtime regression | none>
- summary: <finding summary or none>

ADR or doc follow-up:
- <needed follow-up or none>

Blockers or residual risk:
- <risk or none>

Next action:
- <next step>
```
