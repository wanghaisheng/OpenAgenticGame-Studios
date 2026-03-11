<!-- input: current harness behavior, recent task outcomes, and workflow drift signals -->
<!-- output: a periodic self-assessment checklist for the repo-local Codex layer -->
<!-- pos: maturity self-check for the repo-local harness -->
# Maturity Checklist

Use this file as a periodic self-check for whether the harness is getting stronger or only more verbose.

## Core Questions

- Are `Quick` tasks usually staying within a single coherent milestone?
- Are substantial tasks consistently escalating to `BMM` instead of stretching `Quick`?
- Are required validation packages and hard gates being named explicitly at closeout?
- Are failing builds and audits being diagnosed from evidence before code changes?
- Are change records staying in one primary truth source?
- Are docs staying aligned with behavior and workflow changes?

## Strong Signals

- most bounded tasks close with clear command evidence
- major changes leave usable `openspec/changes/...` records
- compatibility shims are periodically removed instead of only added
- repo-local workflow docs are used more often than copied reference docs
- review summaries consistently mention residual risk, not just happy-path status

## Weak Signals

- repeated ambiguity about whether work belongs in Quick or BMM
- closeouts that say "validated" without naming commands
- large diffs that were never broken into milestones
- repeated reference to `_bmad-output` for new work
- failing builds patched by guesswork instead of diagnosis

## Rule

If the checklist keeps showing the same weakness, change the workflow docs or templates instead of hoping agents remember better next time.
