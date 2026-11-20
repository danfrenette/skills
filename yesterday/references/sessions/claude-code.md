# Claude Code

Each session is one JSON Lines file at `~/.claude/projects/<cwd-slug>/<session-id>.jsonl`, where the
slug is the working directory with `/` replaced by `-`. Subagent transcripts sit in
`<session-id>/subagents/`; skip them.

Find candidates by modification time, then keep files with a user record inside the window:

```bash
find ~/.claude/projects -maxdepth 2 -name '*.jsonl' -newermt '<window start>'
```

Fields to use:

- `type: "user"` with `isSidechain: false` is a user turn, with `timestamp`, `cwd`, and `gitBranch`.
  `message.content` is a string for a typed prompt; an array holds tool results.
- `type: "assistant"` holds replies; read the text blocks in `message.content`.
- `type: "custom-title"` carries `customTitle`.

Typed prompts in the window:

```bash
jq -r 'select(.type=="user" and .isSidechain==false and (.message.content|type)=="string")
  | "\(.timestamp) \(.message.content[0:300])"' <file>
```

Resume command: `claude --resume <session-id>` from the session's `cwd`.
