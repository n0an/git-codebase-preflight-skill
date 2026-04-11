<h1 align="center">Git Codebase Preflight Agent Skill</h1>

<p align="center">
    <img src="https://img.shields.io/badge/git-diagnostic%20workflow-f05032.svg" alt="Git Diagnostic Workflow" />
    <img src="https://img.shields.io/badge/codebase-first%20pass-2d7ff9.svg" alt="Codebase First Pass" />
    <img src="https://img.shields.io/badge/license-MIT-lightgrey.svg" alt="MIT License" />
    <a href="https://agentskills.io/home">
        <img src="https://img.shields.io/badge/Agent%20Skills-Compatible-purple.svg" alt="Agent Skills Compatible" />
    </a>
</p>

An agent skill that helps AI coding agents like Claude Code, Codex, Cursor, and Gemini inspect a repository through git history before opening source files.

It turns a short set of git commands into a repeatable pre-read workflow for spotting churn hotspots, ownership risk, bug clusters, slowing delivery, and firefighting patterns.

It uses the [Agent Skills](https://agentskills.io/home) format, so it works smoothly with Claude Code, Codex, Gemini, Cursor, and more.


## What It Covers

- **Churn Hotspots** - which files changed most in the last year
- **Directory Hotspots** - which folders absorb the most change
- **Ownership Signals** - who built the system and whether maintainers changed
- **Bug Clusters** - which files appear most often in bug-fix commits
- **Lifecycle Signals** - where files are frequently added or deleted
- **Momentum Trends** - whether delivery is steady, declining, or spiky
- **Large Change Spikes** - oversized commits that deserve a closer look
- **Firefighting Patterns** - revert, hotfix, emergency, and rollback frequency
- **Interpretation Guidance** - how to turn git output into a code-reading plan


## Installing

You can install this skill into Claude Code, Codex, Gemini, Cursor, and more by using `npx`:

```bash
npx skills add https://github.com/n0an/git-codebase-preflight-skill --skill git-codebase-preflight
```

If you get the error `npx: command not found`, it means you do not currently have Node installed. You need to run this command to install Node through Homebrew:

```bash
brew install node
```

And if that fails, it usually means you need to [install Homebrew](https://brew.sh) first.

When using `npx`, you can select exactly which agents you want to use during the installation. You can also select whether the skill should be installed just for one project, or whether it should be made available for all your projects.

Alternatively, you can clone this whole repository and install it however you want.


## Using Git Codebase Preflight

The skill is called Git Codebase Preflight, and can be triggered in various ways. For example, in Claude Code you would use this:

> /git-codebase-preflight

And in Codex you would use this:

> $git-codebase-preflight

In both cases you can provide specific instructions if you want only part of the workflow. For example, `/git-codebase-preflight Show me the ownership and bug hotspots` on Claude, or `$git-codebase-preflight Audit this repo before we start refactoring` in Codex.

You can also trigger the skill using natural language:

> Use the Git Codebase Preflight skill to inspect this repository before reading the code.

By default, the skill returns a concise summary in chat. If you want the results saved, ask it to write a report file:

> Use `git-codebase-preflight` and save the report

When asked explicitly, the skill will create `git-codebase-preflight-report.md` in the current working directory.


## Why Use an Agent Skill for This?

Most repository walkthroughs start at the file tree. That is useful, but it misses the operational story hidden in git history.

This skill:
- **Finds risky files early** by combining churn and bug-fix frequency
- **Finds risky folders early** before file-level details get noisy
- **Surfaces ownership gaps** when key contributors are no longer active
- **Shows whether an area is growing, churning, or being repeatedly replaced**
- **Shows delivery patterns** that hint at burnout, stalled projects, or batch releases
- **Guides code reading order** so the first files you open are the ones most likely to matter


## Source Material

This skill is inspired by the article [The Git Commands I Run Before Reading Any Code](https://piechowski.io/post/git-commands-before-reading-code/) by Ally Piechowski, adapted into a structured workflow for coding agents.


## Contributing

Contributions are welcome - whether improving command interpretation, refining heuristics, or adding better examples.

- Keep Markdown concise. There is a token cost to using skills, so respect the token budgets of users.
- Do not repeat things LLMs already know. Focus on signals, tradeoffs, and decision-making heuristics.
- All work must be licensed under the MIT license.


## License

Available under the [MIT License](LICENSE), which permits commercial use, modification, distribution, and private use.
