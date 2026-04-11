# Churn hotspots

Use these commands first to find which files changed most often before reading code.

## Core command

```bash
git log --format=format: --name-only --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

This shows the 20 most frequently changed paths in the selected time window.

## Variants

Use a shorter window for faster-moving repos:

```bash
git log --format=format: --name-only --since="6 months ago" | sort | uniq -c | sort -nr | head -20
```

Use a directory-level pass when file-level churn is too noisy:

```bash
git log --since="1 year ago" --dirstat=files,10,cumulative
```

This helps identify the folders that absorb the most change before drilling into specific files.

Limit to a folder when the user only cares about one area:

```bash
git log --format=format: --name-only --since="1 year ago" -- app/ | sort | uniq -c | sort -nr | head -20
```

Check where new files cluster:

```bash
git log --diff-filter=A --name-only --format='' --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

Check where deleted files cluster:

```bash
git log --diff-filter=D --name-only --format='' --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

## How to interpret it

- High churn means the file attracts repeated change.
- High churn does not automatically mean poor quality. It may reflect active feature work.
- High directory churn means a subsystem is active, even if no single file dominates.
- A lot of added files suggests expansion. A lot of deleted files suggests churn, cleanup, or repeated rework.
- High churn becomes much more concerning when paired with bug-fix frequency from `references/bug-clusters.md`.
- The top 3 to 5 files from this list are the best starting point for code reading.

## What to do next

- Cross-reference the top churn files with bug-fix hotspots.
- Use the directory view first if the repository is large and you need a fast orientation pass.
- Check whether the same files are owned by one or two people.
- Read the highest-churn file first if the user wants to understand where the codebase fights back.
