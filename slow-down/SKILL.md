---
name: slow-down
description: >-
  Slows agent execution so file changes remain easy to follow. Use when the user asks the agent to
  slow down, pace its edits, explain each edit before making it, or change files one at a time.
---

# Slow Down

Keep the user oriented while continuing to make progress.

## Establish The Goal

Infer the session's core goal from the conversation, giving priority to an existing handoff or spec.
Ask the user to confirm the goal only when it remains ambiguous.

The goal is established when it can be stated in one sentence and used to explain why each edit is
necessary.

## Edit Sequentially

For every file edit:

1. In one to three concise sentences, explain how that edit advances the core goal.
1. Edit only that file.
1. Inspect the result before moving to another file.

Treat creating, modifying, deleting, renaming, formatting, and generated changes as edits. When a
command could edit multiple files, replace it with a single-file operation or ask the user before
running it.

Continue this sequence until all necessary edits and verification are complete.
