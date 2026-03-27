# agent-skills

Reusable Claude Code skills for compact session rollover and fresh-session resume.

## What this provides

Two Claude Code skills:

- **`/rollover`** — Checkpoint your current work into a tiny `.agent/resume.md` file and get a bootstrap prompt you can paste into a fresh session.
- **`/rehydrate`** — Resume work in a fresh session by reading `.agent/resume.md`, inspecting git state, and picking up where you left off.

Plus:
- A concise `CLAUDE.md` with stable project policy
- An `.agent/resume.md` template and example
- Hook scaffolding for future automation
- A roadmap for plugins and SDK integration

## Why `/rehydrate` instead of `/resume`?

Claude Code has a built-in `/resume` command for conversation switching. This system uses `/rehydrate` to avoid name collision.

## Installation

### Option A: Copy into your project

Copy the skill folders into your project's `.claude/skills/` directory:

```bash
cp -r path/to/agent-skills/.claude/skills/rollover your-project/.claude/skills/
cp -r path/to/agent-skills/.claude/skills/rehydrate your-project/.claude/skills/
```

Optionally copy the `CLAUDE.md` rules and `.agent/` directory too.

### Option B: Symlink

```bash
ln -s path/to/agent-skills/.claude/skills/rollover your-project/.claude/skills/rollover
ln -s path/to/agent-skills/.claude/skills/rehydrate your-project/.claude/skills/rehydrate
```

### Option C: Shared directory via `--add-dir`

Start Claude Code with this repo as an additional directory:

```bash
claude --add-dir /path/to/agent-skills
```

Skills from added directories are loaded automatically.

**Important:** `CLAUDE.md` files from added directories are **not** loaded unless you set:

```bash
export CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1
```

## Workflow

### Normal work

Work normally in Claude Code. No special setup needed.

### When context gets crowded

Run `/rollover`. It will:

1. Stop at a safe point
2. Inspect git state
3. Write/overwrite `.agent/resume.md` (kept under 20 lines)
4. Return a single fenced `text` block with a bootstrap prompt
5. Recommend `/clear`

### Start fresh

Run `/clear` to start a new session, then either:

- Paste the bootstrap prompt from `/rollover`, or
- Run `/rehydrate`

`/rehydrate` reads `.agent/resume.md`, checks git state, opens the relevant files, and continues from where you left off.

## `.agent/resume.md` format

The resume file uses a fixed schema and is always overwritten (never appended):

```
# Resume

Objective: ...
Next: ...
Files:
- ...

Gotcha: ...
Start with: ...
```

Hard cap: ~20 lines. No history, no completed-task logs, no architecture essays.

## Repository structure

```
README.md
CLAUDE.md
.agent/
  resume.md
.claude/
  skills/
    rollover/
      SKILL.md
    rehydrate/
      SKILL.md
  hooks/
    README.md
examples/
  resume-example.md
docs/
  ROADMAP.md
```

## Future plans

See [docs/ROADMAP.md](docs/ROADMAP.md) for planned enhancements including hooks, plugin packaging, and Agent SDK integration.
