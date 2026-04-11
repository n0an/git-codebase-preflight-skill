# Ownership signals

Use these commands to understand who built the system and whether the people maintaining it now are the same people who shaped it.

## Core command

```bash
git shortlog -sn --no-merges
```

This ranks contributors by commit count across repository history.

## Recent activity window

```bash
git shortlog -sn --no-merges --since="6 months ago"
```

Compare this with the full-history shortlog.

## Who owns a hotspot file now

After identifying a risky file, check who touched it recently:

```bash
git log --since="1 year ago" --format='%an' -- path/to/file | sort | uniq -c | sort -nr
```

This is a practical follow-up to the hotspot scan because it tells you who currently carries that file.

## How to interpret it

- If one person accounts for most commits, there may be bus-factor risk.
- If the top historical contributor disappears from recent history, repository knowledge may have moved or been lost.
- If many historical contributors exist but only a few remain active, the system may now be maintained by a different team than the one that built it.
- If a hotspot file is dominated by one recent author, that area may have concentrated knowledge even if the repo overall does not.

## Caveat

Squash-merge workflows compress authorship. In those repos, shortlog may reflect who merged pull requests rather than who wrote the code. Treat the output as a clue and confirm the team's merge strategy before drawing strong conclusions.

## What to do next

- Compare top contributors against hotspots from `references/churn-hotspots.md`.
- Run the per-file ownership command for the top 3 hotspot files.
- If a risky file seems owned by someone no longer active, prioritize it for documentation and test review.
- Mention bus-factor concerns clearly if the user is planning a refactor or handoff.
