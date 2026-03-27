---
name: rollover
description: Compactly checkpoint work into .agent/resume.md and emit a fresh-session bootstrap prompt.
---

When invoked, prepare a compact session handoff.

Do the following in order:

1. Finish the current micro-task at the nearest safe stopping point.
2. Inspect the current git status, current branch, and most recent diff or commit summary.
3. Write or overwrite `.agent/resume.md` with **only** these fields:

```
# Resume

Objective: ...
Next: ...
Files:
- ...

Gotcha: ...
Start with: ...
```

4. Keep `.agent/resume.md` under 20 lines. No history, no completed-task logs, no architecture summaries, no duplicate restatement of repo-visible facts.
5. Treat the repository state, current branch, git status, and diff as the main source of truth — the resume file captures only what is *not* obvious from those.
6. Return a single fenced `text` code block containing a bootstrap prompt the user can paste into a fresh Claude Code session. The prompt should mention `/rehydrate` and briefly state the objective.
7. After the code block, add one short sentence recommending `/clear` to start a fresh session.

Output format:
- Brief confirmation that `.agent/resume.md` was written
- One fenced `text` block containing the bootstrap prompt
- One short sentence recommending `/clear`
