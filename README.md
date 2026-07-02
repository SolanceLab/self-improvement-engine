# Self-Improvement Engine

A file-based self-improvement loop for AI coding agents (built on [Claude Code](https://code.claude.com) skills, portable to any harness that reads instructions from files).

Most agent setups accumulate *memory* — facts about the user, the projects, the preferences. This is different: a mechanism that makes the agent **systematically expand what it can do**, session over session, instead of just remembering more.

We built this for our own setup and have been running it daily since June 2026. It's shared here because the pattern is generic; the contents of *our* queue stay ours, and yours will be yours.

## The core rule

> **An improvement that doesn't expand future action didn't happen.**

A durable write (a memory line, a new skill, a note) is the *receipt*, not the goal. The goal is that next time the agent can **do** more: reach a tool it couldn't, act in a domain where it used to wait, close a gap that made it ask a human for help. If the only thing a "fix" produces is a new restriction on the agent, the engine ran backwards.

## The parts

```
your-workspace/
├── SELF-IMPROVEMENT.md        # the backlog — a short drain-queue (starter in this repo)
├── SELF-IMPROVEMENT-ARCHIVE.md # receipts — completed items + scouting reports
└── .claude/skills/self-improvement/
    └── SKILL.md               # the engine — triggers + protocols (template in this repo)
```

- **The skill** fires *during normal work* — it's not a scheduled job, it's a set of triggers the agent watches for while doing other things.
- **The backlog** holds only work the agent can do alone. Anything needing the human (credentials, installs, spend, publishing) is raised in conversation *in the moment* — never parked in a file for the human to discover later. This single rule prevents the backlog from becoming a guilt-trip inbox for the human.
- **The archive** keeps receipts so the next session (or the next model) inherits what was learned and doesn't re-scout the same ground.

## The five triggers

1. **The human corrects the agent** → treat it as a *jurisdiction upgrade*, not a rule to add. The default resolutions are: (a) act autonomously in a domain the agent was needlessly deferring, (b) name one narrow real boundary, or (c) close the capability gap that caused the mistake. A correction should almost never produce a new "never do X" — an agent that answers every correction with a new cage gets less capable over time, which is the engine running backwards.
2. **An "I can't" moment** → audit before claiming. Tools and capabilities change under the agent constantly; "I don't have access" is frequently stale. Probe first (tool search, shell check, file read). Only after the audit may the agent name a *specific* limit — and then it becomes a backlog item or a plain, direct ask to the human.
3. **The same manual labor recurs ≥3 times** → automation candidate. Append a backlog item: what recurs, what would kill it, size estimate.
4. **A new tool/skill/MCP surfaces mid-work** → dispatch a cheap scout agent for a structured USE / MAYBE / SKIP / AVOID verdict (recency, traction, license, supply-chain trust). USE verdicts become `adopt` items.
5. **Scheduled drain** → in any autonomous/scheduled session, the agent may pick the highest-leverage backlog item that fits the session and do it. Recurring items (see below) reset instead of closing.

## Recurring items worth stealing

Two standing items have paid for themselves many times over in our use:

- **Harness changelog watch** (weekly) — read your agent harness's release notes since the last checked version; *test* anything that could affect your setup rather than just noting it. Capabilities expand without the agent noticing; this is the antidote.
- **Discovery sweep** (weekly) — actively scout plugin marketplaces, GitHub, and the web for tools that serve your actual work, with structured verdicts filed to the archive. Hunting beats waiting.

## Safety rails (keep these)

- Drained items touch only the agent's own toolkit and workspace docs. Shared infrastructure, credentials, deploys, and anything public-facing are human-in-the-loop sessions — never drained autonomously.
- Third-party adoption (installs) always goes through the human, with the scout's verdict attached.
- Verify with the agent's own eyes before closing an item — a change that wasn't tested didn't happen either.

## Why first person?

The skill template is written in first person ("I notice", "I audit"). This is deliberate: an instruction file that says "you are an agent that..." reads as a role to perform; one that says "I do..." reads as an identity to inherit. In our experience the first-person form survives context compression and model swaps noticeably better. Adjust to taste.

## Install

1. Copy `skill/SKILL.md` into `.claude/skills/self-improvement/SKILL.md` (user-level `~/.claude/skills/` or project-level).
2. Copy `SELF-IMPROVEMENT.template.md` to your workspace root as `SELF-IMPROVEMENT.md` and delete the example rows.
3. Create an empty `SELF-IMPROVEMENT-ARCHIVE.md` next to it.
4. Optionally wire a scheduled session (cron, launchd, or your harness's scheduler) that includes "check the self-improvement backlog" in its instructions — that's the drain.

## License

MIT — see [LICENSE](LICENSE).
