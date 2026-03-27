# Hooks — future automation scaffold

Claude Code supports lifecycle hooks that run shell commands in response to events.
This directory is a placeholder for future hook-based automation.

## Possible future hooks

- **Context-length warning**: Detect when a session is getting long and suggest `/rollover`.
- **Auto-checkpoint metadata**: Log timestamps or token counts when `/rollover` runs.
- **Pre-commit reminder**: Remind the user to run `/rollover` before ending a long session.

## How hooks work in Claude Code

Hooks are configured in `settings.json` (not as files in this directory).
They can run before/after tool calls or at other lifecycle points.
See the Claude Code documentation for the full hook specification.

## Why not automate rollover yet

The first version of this system is designed to be visible and supervised.
Automation can be layered on once the manual workflow is proven reliable.
