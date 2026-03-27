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

## Agent setup (for automated installation)

If you are a Claude Code agent sent here to install these skills into another project, follow these steps exactly.

**Assumptions:** `$TARGET` is the root of the project you are working in. You have already cloned or have access to this repo.

### Step 1: Create directories

```bash
mkdir -p "$TARGET/.claude/skills"
mkdir -p "$TARGET/.agent"
```

### Step 2: Copy skill folders

```bash
cp -r .claude/skills/rollover "$TARGET/.claude/skills/rollover"
cp -r .claude/skills/rehydrate "$TARGET/.claude/skills/rehydrate"
```

### Step 3: Copy the resume template

```bash
cp .agent/resume.md "$TARGET/.agent/resume.md"
```

### Step 4: Verify

Confirm these files exist in the target project:

- `$TARGET/.claude/skills/rollover/SKILL.md`
- `$TARGET/.claude/skills/rehydrate/SKILL.md`
- `$TARGET/.agent/resume.md`

### Step 5: Add to target project's CLAUDE.md

Append the following to the target project's `CLAUDE.md` (create it if it doesn't exist):

```markdown
## Session continuity

- If `.agent/resume.md` exists, read it before making major changes.
- Use `/rollover` to checkpoint when context gets crowded.
- In a fresh session, use `/rehydrate` before continuing.
- Keep `.agent/resume.md` under 20 lines, overwrite-only.
```

### Step 6: Done

The `/rollover` and `/rehydrate` commands are now available. No restart is needed if skills were copied into the project's `.claude/skills/` directory during an active session — they will be discovered on next invocation.

### What the skills do

- **`/rollover`** — Stops at a safe point, writes a compact `.agent/resume.md` (objective, next step, files, gotchas), and returns a bootstrap prompt you can paste into a fresh session. Always recommend `/clear` afterward.
- **`/rehydrate`** — Reads `.agent/resume.md`, inspects git state, opens listed files, and continues work without redoing anything. Use this as the first action in a fresh session.

---

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

## Directing an agent in another repo to install these skills

Add this to the other project's `CLAUDE.md`:

```markdown
## Session continuity

If `.claude/skills/rollover/SKILL.md` does not exist, install session skills:
1. Clone https://github.com/2Beavers/agent-skills.git to a temp directory.
2. Read that repo's README.md and follow the "Agent setup" section to install skills into this project.
3. Remove the cloned temp directory when done.

Once installed:
- Use `/rollover` to checkpoint when context gets crowded.
- In a fresh session, use `/rehydrate` before continuing.
- Keep `.agent/resume.md` under 20 lines, overwrite-only.
```

The agent will clone this repo, read the README, find the mechanical steps, and install the skills into its own project.

## Future plans

See [docs/ROADMAP.md](docs/ROADMAP.md) for planned enhancements including hooks, plugin packaging, and Agent SDK integration.
