# Activity trends

Use commit counts by month to estimate whether the project is steady, declining, accelerating, or shipping in large batches.

## Core command

```bash
git log --format='%ad' --date=format:'%Y-%m' | sort | uniq -c
```

This prints commit count by month across the repository's history.

## Large recent commits

Use this when you want to spot oversized changes that may deserve inspection before reading code:

```bash
git log --since="6 months ago" --shortstat --format='%h %ad %an %s' --date=short
```

This is less about aggregate trends and more about identifying individual large drops.

## How to interpret it

- A steady rhythm usually suggests healthy ongoing delivery.
- A sharp drop over one or two months can hint at staffing changes, reprioritization, or a stalled initiative.
- Large spikes followed by quiet periods often suggest batch releases rather than continuous delivery.
- A long downward slope over 6 to 12 months may indicate fading investment, migration work elsewhere, or team fatigue.
- Very large commits in recent history are often worth reading before source files because they can hide broad refactors, risky merges, or rushed cleanup.

## Caveat

This is team data, not code-quality data. Use it to frame questions and timelines, not to make absolute claims about engineering quality.

## What to do next

- If activity drops sharply, inspect the time period just before the drop for structural changes.
- If activity is spiky, inspect release automation, integration code, and late-stage stabilization work.
- If one or two commits are unusually large, inspect those commits directly before reading affected files in isolation.
- Pair this with ownership signals to see whether momentum changed when key contributors disappeared.
