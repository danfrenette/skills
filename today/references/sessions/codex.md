# Codex

`~/.codex/session_index.jsonl` lists every thread with `id`, `thread_name`, and `updated_at`. Use it
to find candidates updated inside the window and to name them. Each transcript is at
`~/.codex/sessions/YYYY/MM/DD/rollout-<start time>-<id>.jsonl`, filed by start date, so a thread
from an earlier day can continue into the window.

Fields to use:

- The first record is `type: "session_meta"`. `payload.cwd` is the directory, and
  `payload.thread_source` is the origin: keep `user`, and skip `subagent`, `automation`, and
  `guardian_review`.
- `type: "response_item"` with `payload.type: "message"` holds turns. `payload.role` is `user` or
  `assistant`; the text is in `payload.content[].text`.
- Codex also injects context as user messages: text that starts with `# AGENTS.md instructions`,
  `# Files mentioned by the user`, or an XML-style tag such as `<environment_context>`. Skip it; the
  remaining user messages are the user's prompts.

```bash
jq -r 'select(.type=="response_item" and .payload.type=="message" and .payload.role=="user")
  | "\(.timestamp) \(.payload.content[0].text[0:300])"' <file>
```

Resume command: `codex resume <id>`.
