# OpenCode

OpenCode stores sessions in SQLite at `~/.local/share/opencode/opencode.db`. Sibling files such as
`opencode-beta.db` belong to other release channels; check them the same way when they exist.
Current versions write `session_v2` and `session_message`. The older `session`, `message`, and
`part` tables stop receiving data after the migration, so confirm which tables hold the window
before querying.

Top-level sessions updated in the window (times are Unix milliseconds):

```bash
sqlite3 ~/.local/share/opencode/opencode.db "select id, title, directory from session_v2
  where parent_id is null and time_updated >= <window start ms> and time_created <= <window end ms>"
```

User prompts for one session:

```bash
sqlite3 ~/.local/share/opencode/opencode.db "select time_created, json_extract(data, '$.text')
  from session_message where session_id = '<id>' and type = 'user' order by seq"
```

For a full transcript, `opencode session export <id>` prints JSON.

Resume command: `opencode --session <id>` from the session's directory.
