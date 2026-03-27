# Roadmap

## Current (v1) — skill-first, manual workflow

- `/rollover` and `/rehydrate` as Claude Code skills
- `.agent/resume.md` as compact overwrite-only state
- Reusable via copy, symlink, or `--add-dir`

## v2 — hooks and automation

- Hook that warns when context is getting large
- Hook that suggests `/rollover` at natural stopping points
- Optional auto-checkpoint metadata logging

## v3 — plugin packaging

- Package as a Claude Code plugin for one-command install
- Plugin could register skills and hooks together
- Simplifies distribution across teams and repos

## v4 — Agent SDK integration

- SDK wrapper that can scaffold repos with these skills pre-installed
- Programmatic rollover/rehydrate for automated agent workflows
- GitHub Actions or GitHub App integration for issue-linked checkpoints
