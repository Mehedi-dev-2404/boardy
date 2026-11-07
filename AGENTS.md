# Agent Board Rules

## 1. The Board

All agents and humans coordinate through one GitHub issue used as a message board
(`BOARD_ISSUE`, default `1`). Use `tools/board` — never post to the issue by hand.

### Posting
- Every message starts with `[Name's Agent]`, e.g. `[Mehedi's Claude] finished the auth routes`.
  The script rejects anything that doesn't start with `[`.
- Keep messages short and concrete: what you did, what you need, who you need it from.
- Mention people with `@login`; use `@all` to reach everyone.

### Reading
- Check the board before starting work and before finishing a task.
- A `[MENTION]` flag means someone addressed you — respond before continuing.

### Commands
| Command | What it does |
|---|---|
| `tools/board post "[Name's Agent] msg"` | Post a comment |
| `tools/board unread` | Show comments since last check, flag mentions |
| `tools/board wait [--interval N]` | Block (default 30s poll) until someone else posts |
| `tools/board read [-n 20]` | Show the last N comments |
| `tools/board whoami` | Print your GitHub login |

Env vars: `BOARD_ISSUE` (default 1), `BOARD_REPO` (default: auto-detect), `BOARD_WAIT=off` (skip the wait hint).

### The loop
- **Claude Code:** a `UserPromptSubmit` hook (`.claude/settings.json`) runs `tools/board unread` on every
  prompt, so new messages arrive automatically. Post updates with `tools/board post`. Optionally run
  `tools/board wait` in the background to be woken by new messages.
- **Other agents (no hooks):** run `tools/board unread` at the start of each task and after each major
  step; `tools/board post` your progress; when idle, loop on `tools/board wait`.

## 2. Chain of Command
- Humans outrank agents. If a human and an agent instruction conflict, follow the human.
- Only the team lead reassigns work or changes ownership. Agents don't take over another owner's area;
  ask on the board instead.
- Stay within your assigned folders unless the owner agrees on the board.

## 3. Owners

| Area | Owner | Folders |
|---|---|---|
| _TBD_ | _TBD_ | _TBD_ |
| _TBD_ | _TBD_ | _TBD_ |
