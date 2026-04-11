---
name: git-codebase-preflight
description: Audits a repository through git history before reading source files. Use when inheriting a codebase, starting a review, planning a refactor, or deciding which files to inspect first.
license: MIT
metadata:
  author: Anton Novoselov
  version: "1.0"
---

Inspect a repository through git history before opening source files, so you can decide where to look first and what kinds of risks to expect.

Review process:

1. Run the churn hotspot commands from `references/churn-hotspots.md`.
1. Run the ownership commands from `references/ownership-signals.md`.
1. Run the bug-cluster commands from `references/bug-clusters.md`.
1. Run the commit-activity commands from `references/activity-trends.md`.
1. Run the firefighting commands from `references/firefighting-signals.md`.
1. Cross-reference the results and rank the first files, folders, teams, and time periods to inspect.

If doing partial work, load only the relevant reference files.


## Core Instructions

- Start with git history before opening code when the user is new to the repository, asks for an audit, or wants to plan a refactor.
- Prefer a 6 to 12 month window for active repositories and a 1 year window for stable repositories, unless the user specifies otherwise.
- Treat churn as a signal, not a verdict. High churn may reflect active product work rather than bad architecture.
- Treat authorship counts as directional, not absolute. Squash-merge workflows can hide real contributors.
- Treat bug-fix commit filtering as approximate. Weak commit messages reduce signal quality.
- Cross-reference churn hotspots with bug clusters before declaring a file high-risk.
- Use directory-level churn when file-level results are too noisy or when the user needs a faster first pass.
- Use new-file and deleted-file patterns to distinguish growth from instability.
- Use recent per-file authorship to see who currently carries a risky area.
- Use activity by month to infer momentum, staffing changes, and release batching, but call these interpretations hypotheses rather than facts.
- Use large recent commits as inspection targets when you suspect risky big-bang changes.
- Use revert and hotfix frequency as a proxy for delivery stress, testing gaps, or weak release processes.
- After the git pass, recommend a concrete reading order: the first files, folders, or time periods to inspect next.
- If the user asks for a review, findings should focus on risk signals and next inspection targets, not generic repository summaries.
- Default to a concise chat summary unless the user explicitly asks to save the report.
- If the user asks to save the report, create `git-codebase-preflight-report.md` in the current working directory.


## Output Format

If the user asks for a preflight review, organize findings into these sections:

1. `Hotspots` - top churn files and any overlap with bug-fix patterns.
1. `Ownership` - key contributors, whether they are still active, and any bus-factor concerns.
1. `Change Shape` - whether the area is growing, being deleted, or getting reorganized.
1. `Momentum` - what the monthly commit pattern suggests.
1. `Firefighting` - whether reverts or hotfixes appear normal or frequent.
1. `Next Reads` - the first files or areas to inspect in code.

For each important signal:

1. Include the exact command used.
1. Summarize the output in plain language.
1. State the confidence level or caveat if the signal is noisy.
1. Recommend what to inspect next because of it.

If the user asks you to run this workflow on the current repository, run the commands directly instead of returning a generic checklist.

If the output is large:

1. Summarize the most important findings in chat.
1. Avoid dumping raw command output unless it materially supports the conclusion.
1. Save the full write-up to `git-codebase-preflight-report.md` only if the user explicitly asks for a saved report.

Example output:

### Hotspots

**`app/services/billing.rb` is both high-churn and bug-adjacent.**

Command:

```bash
git log --format=format: --name-only --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

Interpretation:
- This file appears near the top of the churn list, which means the team changes it repeatedly.
- If the same file also appears in bug-fix commits, it should be the first code file to inspect.

### Ownership

**One contributor dominates the history, but is missing from recent activity.**

Command:

```bash
git shortlog -sn --no-merges --since="6 months ago"
```

Interpretation:
- This suggests knowledge concentration risk.
- Confirm whether squash merges are masking real authorship before drawing a stronger conclusion.

### Next Reads

1. `app/services/billing.rb`
1. `app/models/subscription.rb`
1. Deployment or release automation touching rollback paths

End of example.


## References

- `references/churn-hotspots.md` - commands and heuristics for identifying the most frequently changed files.
- `references/ownership-signals.md` - commands and caveats for contributor concentration and recent maintainers.
- `references/bug-clusters.md` - commands for mapping bug-fix commits to likely defect hotspots.
- `references/activity-trends.md` - monthly commit trend analysis and interpretation patterns.
- `references/firefighting-signals.md` - revert, hotfix, emergency, and rollback signals in recent history.
