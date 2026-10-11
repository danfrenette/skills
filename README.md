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

- **`periodic-work`:** Runs daily, weekly, or monthly project instructions from an editable
  registry, with one subagent per project.

- **`slow-down`:** Keeps agent edits sequential and explains how each one advances the session goal.

- **`ticket-writer`:** Turns requirements, bugs, chores, or diffs into Linear tickets.

- **`yesterday`:** Assembles an ephemeral standup update from the prior workday.

- **`today`:** Assembles an ephemeral daily plan of to-dos, goals, and starting prompts.

These standalone skills live at `<skill-name>/SKILL.md`. The Anaphor family lives under
`skills/software-factory/`, with each skill at `skills/software-factory/<skill-name>/SKILL.md`.

## Anaphor

Anaphor is a software-delivery workflow for agents. Give it an accepted product spec and a working
repository; it implements the change, reviews it from separate perspectives, verifies real behavior,
and delivers a draft PR with a linked explanation.

Product decisions stay in the accepted spec. Workspace provisioning stays in the project's own
instructions. The workflow uses the host's tools and selected model, with parallel workers where
available and sequential review passes when capacity is limited.

### Install the family

Install all nine skills together so their sibling references resolve:

```bash
npx skills@latest add danfrenette/skills --skill \
  anaphor anaphor-compare-designs anaphor-implement-slices anaphor-review \
  anaphor-verify anaphor-create-feature-map anaphor-audit-feature-map \
  anaphor-explain-change anaphor-reconcile
npx skills@latest add mattpocock/skills --skill \
  tdd code-review handoff writing-for-agents domain-modeling
```

Choose your target agent and installation scope when prompted. The first command installs from the
repository's default branch; to try unmerged work, install from that branch's GitHub URL instead.
The [family guide](skills/software-factory/anaphor/README.md) explains source resolution and
conditional dependencies.

### Start a run

Invoke `anaphor` explicitly with a spec path or issue reference and the owning repository paths. For
example, in a harness with skill mentions:

```text
$anaphor Implement docs/specs/saved-searches.md in this repository.
Use the testing boundaries already agreed in the spec and the setup instructions in AGENTS.md.
```

A spec from Matt Pocock's `to-spec` is the expected input. Include accepted behavior and confirmed
test boundaries; the workflow does not repeat product discovery. Missing product decisions pause the
affected work while independent work can continue.

### How work moves through the factory

1. Establish observable acceptance criteria, repository baselines, testing boundaries, and
   verification routes.
2. Implement the smallest verifiable change with TDD, or organize larger work into dependent slices.
   Compare alternatives when an implementation decision remains unresolved.
3. Review the complete change through Standards, Spec, and Principles. Add execution, security,
   concurrency, migration, and performance passes when their triggers apply.
4. Run repository checks and real user flows. Update affected feature-map recipes and execute them
   against the delivered behavior.
5. Reconcile affected product, domain, setup, and tracker records against decisions and evidence.
6. Open draft PRs and publish a durable walkthrough connecting behavior, decisions, code, and
   verification evidence. Ready-for-review, merge, and deployment remain user decisions.

Required verification cannot be replaced with reviewer agreement. Product failures return to
implementation. If a required browser or environment prerequisite remains unavailable after one safe
recovery attempt, the run stops and reports the block before PR delivery.

### The skills

- **[anaphor][anaphor]:** Own the accepted spec through verified delivery.
- **[anaphor-compare-designs][compare-designs]:** Explore alternatives with
  distinct goals and compare their constraints, callers, tradeoffs, and evidence.
- **[anaphor-implement-slices][implement-slices]:** Sequence dependent slices and
  verify the integrated result before dispatching dependent work.
- **[anaphor-review][review]:** Run separate review perspectives with sourced
  language and interface guidance.
- **[anaphor-verify][verify]:** Execute tests and real flows, retain evidence, and
  distinguish defects from unavailable prerequisites.
- **[anaphor-create-feature-map][create-feature-map]:** Add missing verification
  recipes for affected behavior and prove they work.
- **[anaphor-audit-feature-map][audit-feature-map]:** Audit an entire existing map
  when broader coverage is explicitly needed.
- **[anaphor-explain-change][explain-change]:** Produce an evidence-linked reviewer
  walkthrough, using diagrams or other assets when they clarify the change.

- **[anaphor-reconcile][reconcile]:** Update affected project records after accepted decisions or
  verification, using clear human-facing language and linked evidence.

[reconcile]: skills/software-factory/anaphor-reconcile/SKILL.md
[anaphor]: skills/software-factory/anaphor/SKILL.md
[compare-designs]: skills/software-factory/anaphor-compare-designs/SKILL.md
[implement-slices]: skills/software-factory/anaphor-implement-slices/SKILL.md
[review]: skills/software-factory/anaphor-review/SKILL.md
[verify]: skills/software-factory/anaphor-verify/SKILL.md
[create-feature-map]: skills/software-factory/anaphor-create-feature-map/SKILL.md
[audit-feature-map]: skills/software-factory/anaphor-audit-feature-map/SKILL.md
[explain-change]: skills/software-factory/anaphor-explain-change/SKILL.md

### Review guidance loads by concern

The Principles reviewer selects language profiles from changed behavior. Ruby/Rails draws on
thoughtbot and Sandi Metz; JavaScript/TypeScript draws on Kent C. Dodds and Matt Pocock. Frontend
changes can add Vercel guidance. UI concerns select Emil Kowalski and Jakub Krehel skills, with
Refactoring UI for visual hierarchy and layout. Motion reaches component recipes and interruption
checks only when relevant. The local `emil-unslop-code` lens can also apply outside UI.

The [Principles profiles][principles-profiles] own these triggers and
source-specific adaptations. Installed dependencies are available references, not instructions to
load every skill into every review. Optional local Emil skills must be installed separately on each
machine; the public dependency lock does not reproduce that collection.

[principles-profiles]: skills/software-factory/anaphor-review/references/principles/README.md

### Project setup and ongoing use

Point project instructions to the existing environment setup, test commands, browser access, and
feature maps. Anaphor uses those procedures without requiring a particular tracker, database,
package manager, or model roster. Matt's `handoff` handles user-requested continuation in a fresh
session; it does not replace the published PR walkthrough.

For frequent development, keep a Git checkout on each machine and link the nine Anaphor directories
into that harness's supported skill directory. Pulling the checkout then updates those links. Copy
installations need an explicit update or reinstall; the source checkout alone does not update them.
External and user-supplied skills have their own installation lifecycle.

Anaphor is inspired by **Lauren Tan's pstack** and **Matt Pocock's skills**.
[Attribution](skills/software-factory/anaphor/ATTRIBUTION.md) records sources, deliberate
adaptations, and license notices.
Structural checks have passed; end-to-end agent reliability has not yet been established through
live implementation trials. Change-specific verification belongs in the PR that introduces it.

## Project dependencies

[skills-lock.json](skills-lock.json) records the project-local external skills used to develop and
review Anaphor. Restore them from this repository's root:

```bash
npx --yes skills@1.7.0 experimental_install
npx --yes skills@1.7.0 list --json
```

The CLI installs into `.agents/skills/`, which is ignored by Git and Prettier. Its catalog discovery
excludes locked dependencies there, so they are not republished as this repository's own skills.
Commit the generated lock; keep local adaptations in the Anaphor references and profiles.

The repository also includes Matt Pocock's upstream `retro` and its `writing-for-agents` dependency
for explicitly requested retrospectives on skill-development sessions. Supply session evidence and,
when relevant, Anaphor's implementation brief and verification receipts. This is a repository
development tool, not a required phase or transitive dependency of the Anaphor family.

The lock records sources and content hashes. With floating upstream references, restore can fetch
newer content; review resulting lock changes before adoption. It is not a frozen package restore,
and installing Anaphor elsewhere does not automatically install these dependencies.

Management and review of this skillset belong to the external review mechanism. The source
attribution records design provenance; this repository does not maintain an upstream-review loop.

## License

MIT. See [LICENSE](LICENSE).
