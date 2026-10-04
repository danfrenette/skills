# Software factory: pstack and Matt Pocock research

Inspected **2026-10-04**. This is source review, not a benchmark of either workflow. Upstream
instructions were read as research material; they were not executed. No skills were installed or
changed.

## Sources and revisions

- **Source:** Official `cursor/plugins`, `pstack/`

  **Inspected revision:** `e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a`

  **Version and timestamp:** pstack **0.15.9**; commit 2026-10-03 17:06:48 -07:00, or 2026-10-04 UTC

- **Source:** Official `mattpocock/skills`

  **Inspected revision:** `24fe0ef7737efae15c87225755e9f6f5965e4888`

  **Version and timestamp:** plugin **1.3.1**; commit 2026-10-04 13:48:05 +01:00

Sources: [pstack manifest][p-manifest], [pstack revision][p-commit], [Matt manifest][m-manifest],
[Matt revision][m-commit]. Public repositories were fetched and source files read at these
revisions. Search results lagged pstack at 0.15.5, demonstrating why the live revision matters.
These are the current revisions observed during this research, not a claim about future releases.

## Main finding

**Use pstack's ownership, briefs, task dependencies, and revision-bound evidence; use Matt's
reusable engineering disciplines; make the factory own the verification and feature-map completion
contract.** Neither upstream should become a wholesale dependency.

Current pstack verification is stronger than a broad dismissal would suggest. It explicitly requires
real-surface checks, rejects inconclusive results, generates executable feature maps, audits every
mapped feature live, and records orchestration verification against exact head SHAs. The gaps
relevant here are how consistently those mechanisms are wired into everyday delivery and how much
confidence the review machinery assigns to model agreement. [Feature][p-feature], [verification
creation][p-create], [verification maintenance][p-maintain], [orchestration][p-orch],
[interrogate][p-interrogate].

## Pstack architecture worth carrying forward

1. **Router plus disclosed playbooks.** `poteto-mode` routes investigations, features, bugs,
   prototypes, long runs, PR management, and programs into separate playbooks. Reusable disciplines
   live in leaf skills. The useful structural idea is keeping task-specific sequencing out of the
   coordinator's main body. The current router also has many unconditional triggers and
   dependencies; copying it would import considerable ceremony. [Coordinator][p-mode].
2. **Lead owns design and verification; workers own bounded implementation.** Feature work first
   grounds the subsystem, explores designs, states blocking steps/independent work/shared
   state/decomposition, then delegates implementation. Coupled feature work has one owner, who can
   split internally after prerequisites. [Feature][p-feature].
3. **Fresh context and explicit handoff.** New work defaults to a fresh agent with consolidated
   scope, prior directives, reports, and branch information. Stateful work can justify reuse.
   Parents own the result and inspect the diff rather than relaying a completion claim.
   [Coordinator, Subagents][p-mode].
4. **Distinct fan-out shapes.** `swarm` distinguishes coverage partitions from races and mixed work;
   it declares the selection rule first. `arena` builds alternatives, judges them against a rubric,
   selects a base, deliberately integrates useful ideas, and verifies the synthesized artifact.
   [Swarm][p-swarm], [Arena][p-arena].
5. **Programs use a rolling ready frontier.** Orchestrate scopes units, pilots one through the
   entire path, refills workers as units finish, drains completion events at stable boundaries, and
   integrates continuously. Sub-coordinators are reserved for scale. Each writable artifact has one
   owner. Its brief covers goal, scope, context, acceptance, verification, timebox, constraints,
   report, and standing orders. [Orchestrate][p-orch].
6. **Verification belongs to a revision.** The program ledger keys verdicts by PR and head SHA. A
   changed head invalidates the old verdict; blocked is not pass; behavioral work requires more than
   a type check. Cheap checks can run with the worker; expensive or consequential verification gets
   a separate verifier. [Orchestrate, Verification][p-orch].
7. **Ceremony scales down.** The program playbook explicitly collapses to ordinary execution if one
   agent can finish in the session budget. Its TSV/JSON state, cloud placement, Graphite stacker,
   ledger CLI, and watcher machinery should not become the minimum factory. [Orchestrate][p-orch].

Recommended minimum: one coordinator, a task graph only when useful, one writer per shared checkout,
bounded reviewer/verifier packets, a small evidence record. Add program state only when recovery or
scheduling actually needs it.

## What to change in verification

- **Current upstream evidence:** Feature step 5 says to verify the matching surface; its completion
  sequence does not explicitly update affected feature maps. [Source][p-feature]

  **Consequence for this factory:** Make affected feature-map maintenance and execution of changed
  recipes an explicit completion requirement. This is our added policy, not an upstream guarantee.

- **Current upstream evidence:** Verification creation discovers existing harnesses first, writes
  launch/doctor/drive/evidence/cleanup instructions, seeds 3–5 features, and executes **one** mapped
  feature before handoff. [Source][p-create]

  **Consequence for this factory:** Preserve discovery and proof standards. Mark unexecuted recipes
  as unverified; one successful recipe does not validate the whole initial map.

- **Current upstream evidence:** Maintenance gives every feature a source-reading agent and requires
  a live pass across all features, preserving evidence through teardown. [Source][p-maintain]

  **Consequence for this factory:** Keep a full-map audit as a separate operation. Ordinary
  implementation updates and verifies the affected entries, without auditing the entire app every
  time.

- **Current upstream evidence:** Maintenance outputs `clean`, `changed`, or `blocked`, while
  separately distinguishing product gaps from doc drift. [Source][p-maintain]

  **Consequence for this factory:** Separate documentation outcome from product verdict. A clean map
  can correctly describe a failing product; report both without implying a product pass.

- **Current upstream evidence:** The proof principle favors actual artifacts and rerunnable
  deterministic checks. [Source][p-proof]

  **Consequence for this factory:** Keep tests and asserted browser flows as the evidence
  foundation. Screenshots illustrate visual outcomes; they do not prove persistence or error
  handling alone.

- **Current upstream evidence:** Interrogate elevates consensus across models; arena treats
  convergence as a strong signal. [Interrogate][p-interrogate], [Arena][p-arena]

  **Consequence for this factory:** Treat agreement as review context, not a pass criterion. One
  reproducible defect outranks several approvals; runnable evidence outranks agent confidence.

The generic verification layer should prefer the repo's tests and browser harness, then use
available agent-browser/Playwright tooling for relevant live flows. The universal instruction is to
exercise and assert the actual behavior; tool command syntax and authentication instructions come
from the installed tool and project. This research did not independently audit those browser tools'
current APIs.

Provisioning remains separate. Execution receives a checkout/revision, app target, access
prerequisites, and readiness procedure. It can start or health-check the target as documented;
environment creation, credential provisioning, database cloning, and infrastructure recovery belong
to the project's workspace procedure. Verification reports a failed prerequisite precisely and
resumes after setup resolves it.

## Matt Pocock: useful references and cautions

The current library distinguishes user-invoked orchestration from model-invoked discipline. Its own
mechanics say another skill can invoke model-invoked skills, while user-invoked skills are for
explicit human invocation. That is the upstream composition convention, not a claim that every
harness implements discovery identically. [Engineering catalog][m-catalog], [Skill
mechanics][m-mechanics].

- **Factory need:** Design vocabulary and testable interfaces

  **Current source:** [`codebase-design`][m-design]

  **Recommended relationship:** Reference when choosing module interfaces/seams. It is reusable
  reference, not a workflow to run for every edit. Review its strict vocabulary and seam policies
  before making them universal.

- **Factory need:** Meaningfully different alternatives

  **Current source:** [`DESIGN-IT-TWICE.md`][m-twice]

  **Recommended relationship:** Strong pattern for perspective diversity: separate agents get
  different design constraints, with no model brands required. Adapt its fixed 3+ agents to the task
  budget; all candidates must meet the same requirements and standards.

- **Factory need:** Small verifiable increments

  **Current source:** [`tdd`][m-tdd]

  **Recommended relationship:** Reference if accepting its exact policy. It requires user-confirmed
  seams before writing tests, postpones refactoring to review, and rejects database side-channel
  assertions. Those are current upstream rules, not merely local customizations. An autonomous
  factory may need its own attributed testing discipline rather than silently overriding these
  policies.

- **Factory need:** Bug reproduction and proof

  **Current source:** [`diagnosing-bugs`][m-debug]

  **Recommended relationship:** Strong direct augmentation: a runnable, symptom-specific failing
  loop, minimization, falsifiable hypotheses, regression proof, and rerunning the original scenario.
  It is deliberately demanding; route hard bugs here rather than every trivial fix.

- **Factory need:** Separate review perspectives

  **Current source:** [`code-review`][m-review]

  **Recommended relationship:** Standards and Spec run in separate contexts, with no model diversity
  requirement. Useful pattern. Exact skill expects tracker setup and a supplied fixed point, and
  requires preserving its two output axes; do not call it while silently discarding those rules.

- **Factory need:** Domain decisions

  **Current source:** [`domain-modeling`][m-domain]

  **Recommended relationship:** Reference when changing terminology or domain relationships. It
  updates glossary/ADRs lazily; reading existing terminology alone does not trigger the full skill.

- **Factory need:** Resolve an empirical design question

  **Current source:** [`prototype`][m-prototype]

  **Recommended relationship:** Reference for throwaway logic/state or UI experiments. It has
  specific artifact and capture conventions, so use only when those match the requested experiment.

- **Factory need:** Evidence in handoff

  **Current source:** [`pr`][m-pr]

  **Recommended relationship:** Useful before/after proof and reversibility/blast-radius guidance.
  Keep the project's PR template and user's requested delivery format authoritative; do not impose a
  visual summary on every tiny change.

- **Factory need:** Decomposition and scheduling

  **Current source:** [`to-tickets`][m-tickets], [`implement-spec`][m-implement-spec]

  **Recommended relationship:** Architecture references, not automatic nested calls: both are
  user-invoked. Borrow vertical slices, explicit blockers, ready frontier, separate worktrees, and
  integration ownership into the factory's own process. Avoid importing tracker setup or human
  approval gates by accident.

Current naming matters: `to-prd` became `to-spec`; `to-plan` and `to-issues` merged into
`to-tickets`; `design-an-interface` moved into `codebase-design/DESIGN-IT-TWICE.md`. These are
documented in the [changelog][m-changelog]. References to old standalone skills would be stale.

`implement-spec` is especially relevant: independent implementers work tickets on branches based on
an integration branch, merge the integration tip before returning, and a merger integrates them;
ready tickets are dispatched as blocking edges clear. It performs a final code review. The inspected
text does not itself establish an explicit post-merge runtime/test proof gate, so add one in this
factory. [Source][m-implement-spec].

## Model-independent orchestration

Pstack already permits `inherit-parent` and `auto` aliases in role and panel configuration.
Therefore it is inaccurate to say it cannot run with one model. However, its explanation of why
review works remains explicitly multi-model: Interrogate says the adversarial signal comes from
model diversity rather than personas, uses identical briefs, and emphasizes consensus. Orchestrate
requests a verifier from another family for substantial work. [Setup][p-setup],
[Interrogate][p-interrogate], [Orchestrate][p-orch].

Our design should instead make task and evidence diversity the default:

- **Role:** Builder

  **Receives:** Accepted requirements, scoped paths, current revision, relevant project conventions

  **Produces:** Implementation plus commands run and known gaps

- **Role:** Spec reviewer

  **Receives:** Accepted requirements, feature map, pinned diff/source

  **Produces:** Missing/incorrect requirements, unintended behavior, source evidence

- **Role:** Standards/design reviewer

  **Receives:** Project standards, applicable design decisions, pinned diff/source

  **Produces:** Concrete violations and separately labeled design judgments

- **Role:** Runtime verifier

  **Receives:** Acceptance criteria, feature recipes, current target/revision

  **Produces:** Executed tests/flows, expected and observed results, artifacts, explicit gaps

- **Role:** Additional risk reviewer

  **Receives:** A triggered concern such as authorization, concurrency, migration, or shared state

  **Produces:** Counterexamples and evidence specific to that concern

Use the inherited model for every role by default. Model overrides are optional capability choices,
subject to the host and user configuration. Do not require model discovery, premium tiers, or a
provider roster to run the workflow.

Reviewers receive source facts and constraints, but initially omit builder persuasion and other
reviewers' conclusions. That is intended to reduce anchoring; it does not create statistical
independence or prove a quality gain. Independently verify hypotheses before synthesizing. Design
variants should differ in a real constraint (caller simplicity, data ownership, failure model), not
theatrical personas or permission to violate requirements.

With limited concurrency, dispatch the same roles sequentially into fresh contexts. With only one
context available, perform distinct passes and disclose the reduced separation. Do not describe
repeated passes in one conversation as independent reviewers. One model can supply multiple
perspectives; correlated model limitations remain.

In Codex or another harness, use its actual subagent, worktree, execution, and browser interfaces.
Cursor `Task`, cloud placement, plugin dependencies, and `.cursor` paths are not portable contracts.
The workflow specifies required capabilities and records unavailable coverage; an adapter or the
host's own instructions supply the mechanism.

## Recommended end-to-end flow

1. **Frame:** pin intent and observable acceptance criteria; locate relevant feature-map entries and
   project setup/verification pointers.
2. **Ground:** inspect the affected behavior and constraints. Use a prototype or independent design
   alternatives when an unresolved decision warrants them.
3. **Slice:** form independently verifiable slices and blocking edges. Start with one slice that
   exercises the full path; avoid program bookkeeping for one small change.
4. **Build:** one writer per shared target. Run focused behavior tests; use an observed red-to-green
   loop for bugs and test-first work.
5. **Review:** fresh Spec and Standards/design contexts; add a risk perspective only for a concrete
   risk. Evaluate findings on evidence, not vote count.
6. **Verify:** run the applicable tests and real browser/service/CLI flow at the delivered revision,
   including the relevant failure and persistence behavior. Rerun affected checks after fixes and
   integration.
7. **Maintain the map:** update changed entries, add new behavior, remove obsolete routes, and
   execute altered recipes. Keep document status separate from product correctness.
8. **Close:** report criterion → action → expected → observed → evidence → revision, with `pass`,
   `fail`, `blocked`, or `not run`. Completion requires the applicable checks and map updates; a
   blocked check is an explicit gap.

For uncommitted changes, record a reproducible tree/diff identity as well as HEAD; HEAD alone cannot
identify what was executed. Keep receipts small and file-based initially. Revisions plus proof
obligations matter more than a custom orchestration database.

## Composition policy and next validation

Reference reusable installed disciplines through explicit trigger pointers. Keep local feature maps
and setup facts in the project. If an upstream rule conflicts with the factory's accepted policy,
choose an attributed local adaptation or leave that skill optional; do not claim full invocation
while quietly dropping its requirements. User-invoked upstream flows remain optional entry points
and architecture references.

Record upstream revision/license provenance when copying or adapting text, and define an intentional
update process. Both inspected manifests specify MIT, but copying still requires preserving
applicable notices. Avoid a live `main` dependency that changes behavior unnoticed.

Before implementation, settle three policy choices: whether to adopt Matt's mandatory seam
confirmation; where project feature-map pointers live; and how much review a small change warrants.
User agreement already settles the larger boundary: provisioning stays local, while real
verification and affected feature-map maintenance remain factory responsibilities.

Validate with a library fix, a browser feature with persistence, and a multi-repo change that needs
Marketfuel setup. Compare fresh same-model role runs against a single-context baseline. Measure
missed acceptance criteria, reproducible defects found, unsupported completion claims, cost, and
blocked-check honesty. This research makes no measured claim that more agents or particular role
labels improve quality.

[p-manifest]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/.cursor-plugin/plugin.json
[p-commit]: https://github.com/cursor/plugins/commit/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a
[p-mode]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/poteto-mode/SKILL.md
[p-feature]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/poteto-mode/playbooks/feature.md
[p-orch]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/poteto-mode/playbooks/orchestrate.md
[p-swarm]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/swarm/SKILL.md
[p-arena]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/arena/SKILL.md
[p-interrogate]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/interrogate/SKILL.md
[p-create]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/create-verification-skill/SKILL.md
[p-maintain]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/maintain-verification-skill/SKILL.md
[p-proof]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/principle-prove-it-works/SKILL.md
[p-setup]:
  https://github.com/cursor/plugins/blob/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack/skills/setup-pstack/SKILL.md
[m-manifest]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/.claude-plugin/plugin.json
[m-commit]: https://github.com/mattpocock/skills/commit/24fe0ef7737efae15c87225755e9f6f5965e4888
[m-catalog]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/README.md
[m-mechanics]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/productivity/writing-for-agents/SKILL-MECHANICS.md
[m-design]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/codebase-design/SKILL.md
[m-twice]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/codebase-design/DESIGN-IT-TWICE.md
[m-tdd]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/tdd/SKILL.md
[m-debug]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/diagnosing-bugs/SKILL.md
[m-review]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/code-review/SKILL.md
[m-domain]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/domain-modeling/SKILL.md
[m-prototype]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/prototype/SKILL.md
[m-pr]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/pr/SKILL.md
[m-tickets]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/to-tickets/SKILL.md
[m-implement-spec]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/skills/engineering/implement-spec/SKILL.md
[m-changelog]:
  https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/CHANGELOG.md
