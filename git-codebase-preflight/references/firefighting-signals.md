# Firefighting signals

Use revert and hotfix patterns to estimate how often the team ships under stress.

## Core command

```bash
git log --oneline --since="1 year ago" | grep -iE 'revert|hotfix|emergency|rollback'
```

This surfaces commits that look like rollback or emergency-response work.

## How to interpret it

- A few results in a year is normal.
- Frequent reverts or hotfixes suggest weak test coverage, missing staging confidence, or a painful deploy process.
- Zero results is still a signal. It may mean the team is stable, or it may mean commit messages are vague.

## Caveat

This check depends heavily on commit naming habits. If the team writes bland messages, report low confidence instead of over-interpreting the absence of matches.

## What to do next

- If this list is busy, inspect deployment code, CI, release scripts, and the highest-risk files from the hotspot analysis.
- Mention the likely operational follow-up: test reliability, staging parity, and rollback ergonomics.
- If the user wants a deeper audit, read a few revert or hotfix commits directly after this pass.
