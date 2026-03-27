---
name: rehydrate
description: Resume work from .agent/resume.md, current git state, and listed files.
---

When invoked in a fresh session, do the following:

1. Read `.agent/resume.md`.
2. Inspect git status and the latest relevant diff or commit summary.
3. Open the files listed in `.agent/resume.md`.
4. Briefly restate:
   - the objective
   - the immediate next step
   - any important gotcha
5. Continue from there without redoing completed work.
6. Preserve the current approach unless a clear issue appears.
7. Keep future updates to `.agent/resume.md` compact and overwrite-only.

If `.agent/resume.md` is missing, say so clearly and ask the user whether to proceed from repo state alone.
