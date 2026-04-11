# Bug clusters

Use bug-related commit messages to approximate where defects concentrate.

## Core command

```bash
git log -i -E --grep="fix|bug|broken" --name-only --format='' | sort | uniq -c | sort -nr | head -20
```

This highlights the files most often touched by commits that look bug-related.

## Variants

Use a time window if the repository is old or the user cares about current behavior:

```bash
git log -i -E --grep="fix|bug|broken" --since="1 year ago" --name-only --format='' | sort | uniq -c | sort -nr | head -20
```

Adjust keywords if the team uses different language:

```bash
git log -i -E --grep="fix|bug|broken|issue|defect|regression" --name-only --format='' | sort | uniq -c | sort -nr | head -20
```

## How to interpret it

- A file that appears high on both the churn list and the bug-fix list is usually your clearest risk signal.
- A high bug count with low churn can suggest a fragile subsystem that rarely changes but breaks when touched.
- Weak commit-message discipline lowers confidence, so say that explicitly when the results look sparse or noisy.

## What to do next

- Cross-reference the top bug-cluster files with `references/churn-hotspots.md`.
- Read the commit history for the worst overlapping file before opening the source.
- If the same path keeps appearing, look for missing tests, brittle dependencies, or patch-on-patch design.
