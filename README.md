# skills

My agent skills catalog, following the [Agent Skills](https://agentskills.io) convention. Works with
the generic [`skills`](https://github.com/vercel-labs/skills) CLI and any agent that supports the
convention, including OpenCode.

## Install

```bash
npx skills@latest add danfrenette/skills
# or
pnpm dlx skills add danfrenette/skills
```

The installer discovers the skills in this repository, lets you pick which to install, and prompts
for a target agent (OpenCode supported).

## Skills

- **`commit-writer`:** Generates conventional git commit messages from staged or unstaged changes.

- **`morning`:** Follows a Markdown morning checklist using existing scripts and skills.

- **`slow-down`:** Keeps agent edits sequential and explains how each one advances the session goal.

- **`sync-opencode-fork`:** Rebases the OpenCode `dan-dev` fork onto V2, then production after
  release.

- **`ticket-writer`:** Turns requirements, bugs, chores, or diffs into Linear tickets.

- **`yesterday`:** Assembles an ephemeral standup update from the prior workday.

- **`today`:** Assembles an ephemeral daily plan of to-dos, goals, and starting prompts.

Each skill lives at `<skill-name>/SKILL.md`.

## Anaphor (draft)

[Anaphor](anaphor/README.md) takes an accepted product spec through implementation, layered review,
tests and real user-flow verification, then delivers a draft PR with a linked walkthrough. Workspace
provisioning stays in project-local instructions.

Install the eight `anaphor` / `anaphor-*` skills together, plus Matt Pocock's `tdd` and
`code-review`. The [family guide](anaphor/README.md) lists their roles and dependencies.

The workflow is openly inspired by **Lauren Tan's pstack** and **Matt Pocock's skills**.
[Attribution](anaphor/ATTRIBUTION.md) records the source revisions, influences, deliberate
adaptations, and upstream license notices. The initial draft has not yet been validated through live
implementation runs.

## Maintaining this repository

[skills-lock.json](skills-lock.json) records the project-local external skills used to develop and
review Anaphor. Restore them from this repository's root:

```bash
npx --yes skills@1.7.0 experimental_install
npx --yes skills@1.7.0 list --json
```

The CLI installs into `.agents/skills/`, which is ignored by Git and Prettier. Its catalog discovery
excludes locked dependencies there, so they are not republished as this repository's own skills.
Commit the generated lock; keep local adaptations in the Anaphor references and profiles.

The lock records sources and content hashes. With floating upstream references, restore can fetch
newer content; inspect any resulting lock changes using [DAILY.md](DAILY.md). It is not a frozen
package restore, and installing Anaphor elsewhere does not automatically install these dependencies.

`DAILY.md` defines staged update checks, compatibility review, validation, and reporting. It also
tracks pstack and other guidance that is referenced rather than installed. Scheduling is separate.

## License

MIT. See [LICENSE](LICENSE).
