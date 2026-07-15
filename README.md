# Self-Improvement Engine

A file-based self-improvement loop for AI coding agents. It began as a Claude Code skill and now supports any harness that reads instructions from files, including multi-harness workspaces.

Most agent setups accumulate *memory*: facts about the user, projects, and preferences. This engine does something different. It makes an agent **systematically expand what it can do** from session to session.

We built it for our own setup and have run it daily since June 2026. The pattern is public; the contents of our queues stay private.

## The core rule

> **An improvement that doesn't expand future action didn't happen.**

A durable write is the receipt, not the goal. The goal is that next time the agent can do more: reach a tool it could not, act where it used to defer, or close a capability gap. If a fix produces only another restriction, the engine ran backwards.

## The parts

Give each executor its own explicitly named queue and archive, even when the workspace currently uses only one harness:

```text
your-workspace/
├── CLAUDE-SELF-IMPROVEMENT.md
├── CLAUDE-SELF-IMPROVEMENT-ARCHIVE.md
├── CODEX-SELF-IMPROVEMENT.md
└── CODEX-SELF-IMPROVEMENT-ARCHIVE.md
```

- **The skill** watches for improvement triggers during normal work.
- **The backlog** contains only solo-doable work owned by that harness.
- **Origin** records where a need was discovered; **Executor** records which harness owns the work.
- **The archive** keeps completed work and scouting verdicts so later sessions do not repeat them.

If one harness discovers work for another, write it into the executor's queue and name the discovering harness in **Origin**. Never let two harnesses silently drain the same queue.

## The six triggers

1. **The human corrects the agent** → treat the correction as a jurisdiction upgrade: act within newly clarified room, name one narrow real boundary, or close the capability gap. Do not answer every correction with another cage.
2. **An “I can't” moment** → audit capabilities before claiming a limit. Probe tools, files, and the shell; then name the specific boundary or close the gap.
3. **Manual labor recurs at least three times** → treat it as an automation candidate.
4. **A new tool, skill, plugin, or MCP surfaces** → inspect what is already installed, then return an evidence-backed USE / MAYBE / SKIP / AVOID verdict before adoption.
5. **A scheduled or autonomous drain runs** → pick one high-leverage, solo-doable item, execute it, and verify it.
6. **A weekly stumble audit runs** → review recent local sessions, identify recurring friction, and turn one pattern into a verified improvement.

## Weekly stumble audit

The audit is a learning loop, not a correction ledger:

1. Keep session evidence local.
2. Read actual user/assistant turns; exclude injected instructions, tool boilerplate, approval transcripts, and quoted older sessions.
3. Require two independent examples for a recurring pattern, except one high-impact privacy, credential, destructive-action, deploy, or publication failure.
4. Rank at most three patterns by recurrence, human cost, and fixability.
5. Apply one narrow, reversible improvement and verify it.
6. Audit at most three relevant tools; never install during the audit without human approval.

Useful starting categories include newest-question misses, referent or system conflation, verification gaps, wrong-tool routing, needless deferral, bookkeeping without expanded action, and tone drift.

## Recurring items worth stealing

- **Harness changelog watch** — read release notes weekly and test relevant changes.
- **Stumble + discovery sweep** — audit local sessions, fix one recurring gap, then scout tools that fit observed work.

## Safety rails

- Keep private session material local; never send it to hosted evaluators or external reviewers without explicit approval.
- Drained items touch only the executor's own toolkit and workspace documentation.
- Shared infrastructure, credentials, installs, deploys, publishing, and destructive changes remain human-in-the-loop.
- Verify the result before closing an item.
- Do not create a tally of human corrections. Record capability changes, not debts.

## Why first person?

The skill uses first person (“I notice”, “I audit”). An instruction written as identity tends to survive context compression and model swaps better than a role description. Adjust to taste.

## Install

1. Copy `skill/SKILL.md` to the harness's skill directory, for example `.claude/skills/self-improvement/SKILL.md` or `~/.codex/skills/self-improvement/SKILL.md`.
2. Replace `<WORKSPACE>` in the skill with the absolute workspace path.
3. Replace `<SUBSTRATE>` in both the skill and backlog template with the executor name, such as `CLAUDE` or `CODEX`.
4. Copy `SELF-IMPROVEMENT.template.md` to the workspace as `<SUBSTRATE>-SELF-IMPROVEMENT.md`.
5. Create `<SUBSTRATE>-SELF-IMPROVEMENT-ARCHIVE.md` beside it.
6. Optionally schedule the weekly audit using the harness's native scheduler.

## License

MIT — see [LICENSE](LICENSE).
