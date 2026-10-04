# Markdown style

Wrap Markdown source at 100 columns for human readability. The Markdown override in
`.prettierrc.json` defines the formatter settings: `printWidth: 100` and `proseWrap: always`.

Keep tables within that width; use labelled lists when their contents need more space. Preserve
unbreakable URLs, link targets, and code whose syntax or meaning would change if wrapped. These are
exceptions to the width limit, not reasons to leave ordinary prose unwrapped.

Downloaded dependencies in `.agents/skills/` retain their upstream bytes and formatting. Manage them
through the skills CLI; put local adaptations in Anaphor's integration references and profiles.

For dependency and upstream-source maintenance, follow [DAILY.md](DAILY.md).
