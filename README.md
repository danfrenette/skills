# skills

Dan Frenette's agent skills catalog, following the [Agent Skills](https://agentskills.io) convention. Works with the generic [`skills`](https://github.com/vercel-labs/skills) CLI and any agent that supports the convention, including OpenCode.

## Install

```bash
npx skills@latest add danfrenette/skills
# or
pnpm dlx skills add danfrenette/skills
```

The installer discovers the skills in this repository, lets you pick which to install, and prompts for a target agent (OpenCode supported).

## Skills

| Skill | Description |
| --- | --- |
| `commit-writer` | Generates conventional git commit messages from staged or unstaged changes. |
| `sync-opencode-fork` | Rebases the OpenCode `dan-dev` fork onto V2, then production after release. |
| `ticket-writer` | Turns requirements, bugs, chores, or diffs into Linear tickets. |
| `yesterday` | Assembles an ephemeral standup update from the prior workday. |

Each skill lives at `<skill-name>/SKILL.md`.

## License

MIT. See [LICENSE](LICENSE).
