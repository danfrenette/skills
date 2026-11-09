# pstack 0.15.36 review for Anaphor

Research date: 2026-11-08. Anaphor baseline: `843e82b` on `refactor/anaphor-progressive-disclosure`,
after the rename to `cross-examine`, `walkthrough`, `create-feature-map`, and `audit-feature-map`.
This is an integration assessment, not an implemented workflow change or a live reliability trial.

## Sources

- **pstack, current:** [cursor/plugins/pstack @ `c742dd6`][pin], full revision
  `c742dd61706fbacc1b95f1a20b7b988cf096ce6c`. The
  [manifest](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/.cursor-plugin/plugin.json)
  reports version 0.15.36. The commit is dated 2026-10-27 ("make Orchestrate agentic and delete the
  orch scripts"). Accessed 2026-11-08 through `gh api`.
- **pstack, previously attributed:** `e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a` (0.15.9) and
  `ea32d9562a1c9f077d7cdd3be53d07383eb18866` (0.15.18). Accessed 2026-11-08 for the diffs below.
- **Author's post, 2026-11-08:** "use /create-formal-verification-skill to model these state
  machines, one skill per subsystem. and use /statechart to visualize my most important user flows",
  with a reply suggesting "find all of the implicit state machines in my app". **Unverified:**
  quoted from the request; the post itself was not opened.
- **Anaphor:** `~/code/skills`, chiefly [anaphor/SKILL.md](../../anaphor/SKILL.md),
  [ATTRIBUTION.md](../../anaphor/ATTRIBUTION.md), the `references/` procedures, and the four renamed
  skills. Style follows the earlier [verification fit assessment](pstack-verification-fit.md).

[pin]: https://github.com/cursor/plugins/tree/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack

## Finding

The new pstack material splits into one substantive capability and several small habits. The
capability is **formal verification as maintained project infrastructure**: a create/maintain pair
that mirrors the feature-map pair Anaphor already adapted, plus a TLA+ charting tool. It addresses a
real gap. Anaphor's Concurrency and Execution passes reason about ordering by inspection, and its
feature recipes prove one observed path, so neither covers every interleaving. The habits are goal
restatement and prompt sharpening. One is cheap and fits; the other conflicts with the accepted-spec
boundary.

The most consequential behavioral change is in an already adapted skill. `interrogate` dropped the
act-on/consider/noted/dismissed lead-judgment model that `cross-examine` inherited. It now keeps
only findings that a rerun command proves. Anaphor should take that rule for runtime passes but not
for its inspection axes.

## New skills

### create-formal-verification-skill

[Source](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/create-formal-verification-skill/SKILL.md).
It picks the repository's highest-cost, least-tested promise and verifies one property with the
cheapest fitting tool: TLA+ by default for ordering, a code-level verifier for per-input properties,
generated-input testing when no verifier exists. It then generates a project-local verify skill
containing a coverage record (files and functions) and a **sync commit**. The rules that matter are:
every model element points to openable code, with atomic steps kept atomic; each property is shown
failing on a broken variant; findings are never weakened into passes; and scope and bounds are
stated. Before hand-off it runs the generated skill on a scratch break of the real code. Product
code is not changed unless asked.

**Fit.** This is a peer to `create-feature-map`, not a part of it. A recipe proves that one observed
journey produces an accepted outcome on a running surface. A formal check proves a property of a
model within stated bounds. They share the lifecycle this repository already uses: create, consume
in delivery, maintain between runs. They also share the rules: an executed result before hand-off, a
project-local location, and failures kept as failures.

| Anaphor owner          | What it would add                                         |
| ---------------------- | --------------------------------------------------------- |
| New formal-check skill | Explicit creation for one named subsystem or property     |
| `verify` (consume)     | Rerun covered checks when a change touches recorded files |
| `cross-examine` passes | Cite an existing model; propose one for risky ordering    |
| `verify/evidence.md`   | Model, bounds, tool version, sync commit in `Target`      |
| `reconcile`            | Coverage record and sync commit as authoritative records  |

**Deliberate choices.**

- _Accepted spec as input._ The property must come from an accepted requirement or a documented
  promise. Upstream's "choose the strongest target in the repo" amounts to product discovery when
  run inside delivery. Keep creation out of ordinary runs. Run it on explicit request, like
  bootstrap, or when an accepted spec names the property. `bootstrap.md` already says "current
  output alone cannot define correctness"; the same rule applies to invariants.
- _Project-owned provisioning._ The tool (TLC with Java, a prover, a fuzzer) is a prerequisite.
  Install it through project setup with a pinned version, never from inside the skill. Upstream's
  "one command, reproducible tool version" agrees with this.
- _Revision-bound evidence._ The sync commit is a revision binding for the model. A check result
  should also record source revision, model revision, bounds, and tool version. A model pass is a
  coverage-limited result for the property. It is never a functional pass for a criterion that needs
  observed behavior.
- _Draft-only PRs._ No conflict. Upstream already puts verification updates in their own change.

**Cost.** This is the heaviest candidate. It needs modeling skill in TLA+, Kani, Dafny, or a similar
tool, and fidelity review of every model-to-code mapping. It adds a tool dependency per project and
a slow first run. The context cost is moderate: the skill is 43 lines, but a useful model requires
reading the whole subsystem. The main risk is a faithful-looking model that is wrong. Upstream's
scratch-break proof and counterexample replay are the mitigation, and both must be kept.

**Recommendation: adapt.** Add consumption first: `verify` reruns any project formal check whose
coverage record intersects the change, and treats a stale sync commit as stale evidence. Add
creation as a separate explicitly invoked skill after one trial on a real subsystem. The tweet's
"one skill per subsystem" matches Anaphor's project-local, host-independent locations. Reference
pstack `/statechart` by name for result reading, as upstream does, rather than copying commands.

### maintain-formal-verification-skill

[Source](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/maintain-formal-verification-skill/SKILL.md).
It brings a verify skill back in line after unchecked merges. Each check gets one or two outcomes:
**in sync**, **updated**, **bug**, or **blocked**; updated and bug can co-occur. The steps are:

1. Run each check as is before editing.
2. Diff the covered files from the sync commit, including renamed or moved code and new writers of
   guarded state.
3. Classify each change as no effect, model drift, an intentional promise change (which needs cited
   evidence), or a possibly broken promise.
4. Update the model from the code, never from the result.
5. Show that each updated pass can still fail.
6. Replay each counterexample against real code before calling it a bug, and name the commit that
   introduced it.

The sync commit advances only for checks that were confirmed. Edits are limited to verification
files.

**Fit.** This maps almost exactly onto
[audit-feature-map maintenance](../../audit-feature-map/references/maintenance.md), whose outcomes
are clean, changed, blocked, and product failure. That procedure also limits edits to verification
assets and returns product defects with the intended assertion. Three ideas are stronger than
Anaphor's current audit and apply to feature maps as well as models:

- **Sync commit.** The map records the commit at which each recipe was last live-proven, so drift
  detection can diff from it instead of relying on a vague recent-change sweep.
- **Intentional promise change needs cited evidence.** Anaphor says "repair against accepted
  behavior" but does not require evidence when the accepted behavior itself has moved.
- **Run as is before editing.** This keeps the stale-pass case visible: "the old pass was on a stale
  description."

**Cost.** Low beyond the creation skill's tool dependency. The added maintenance outcome needs no
new publication contract.

**Recommendation: adapt.** Port the sync commit, the run-first rule, and the cited-evidence rule
into `audit-feature-map` now. Add the formal-check branch of maintenance with the creation skill,
reusing the existing publication contract (one draft corrections PR) and periodic-work scheduling.

### statechart

[Source](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/statechart/SKILL.md)
and
[render reference](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/statechart/references/render.md).
The agent writes a TLA+ spec in which every rule the reader accepts is an `INVARIANT`. It also
writes a view module that maps model states and actions to reader-facing labels such as "Paying" or
"you press play", along with groups, colors, and conditions. A bundled TypeScript command runs TLC,
iterates past broken rules up to a 100,000-state bound, and emits a Mermaid chart (budget 500
states, about 20 arrows) that marks `breaks` and `mayBreak` states. Its report gives the shortest
path to each violation. Rendering to SVG uses `pele@1.9.0`. When the model describes code, every bug
path must be replayed against the real code.

**Fit.** There are two places:

- **[walkthrough](../../walkthrough/SKILL.md):** a statechart of a changed user flow answers "what
  can the user reach now?" better than prose. That suits the tour's question-led visuals.
- **compare-designs:** the same chart can contrast two candidate state models.

It does not belong in spec intake: "the reader decides whether the behavior is right" is a product
decision, which Anaphor returns to the user or leaves upstream.

**Cost.** High, and it conflicts with project-owned provisioning. The runner needs Node 22.18+, Bun
1.1.5+, or Deno 2. Its first run uses mise to install `java@temurin-25` and downloads
`tla2tools.jar` 1.7.4 from GitHub
([`run.ts`](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/statechart/scripts/run.ts),
lines 68-69), so it needs the network. Pele is a further npm install. The skill bundles roughly 30
script files plus a test corpus. The chart is a picture of a model, so a tour must label it as such
and never present it as observed behavior.

**Recommendation: reference only.** When pstack is installed and a project already has a TLA+ model,
`walkthrough` may invoke `/statechart` for a flow visual. The visual must be marked model-derived
and paired with the receipt that replayed any bug path. Do not vendor the scripts or make the tool a
dependency. Revisit if the formal-check skill is adopted and a project's setup provisions TLC.

### sharpen

[Source](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/sharpen/SKILL.md).
A 16-line prompt rewriter. It asks what a top professional would do that the user did not request,
what rawer source material they would start from, which methods and tools they would use, and what
outside oracle would show the result is right. It then rewrites the prompt, leaving the user's
choices open, and does not perform the task.

**Fit.** Poor inside Anaphor. Question 1 deliberately widens the task beyond what was asked, which
is the opposite of an accepted spec plus
[robustness scope](../../anaphor/references/robustness-scope.md). Question 4 is already enforced:
step 1 requires every criterion to have an owning surface and verification route.

**Recommendation: skip** in Anaphor. It may help upstream of `to-spec`, where discovery belongs;
that is the user's tool choice, not a workflow dependency.

### in-your-own-words

[Source](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/in-your-own-words/SKILL.md).
One sentence: restate the user's goals and the problem they are solving. Its weight comes from its
callers. `interrogate` uses it to frame intent, and
[poteto-mode](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/poteto-mode/SKILL.md)
now opens every task with goal, problem, and the smallest change expected. It does not wait for
confirmation, and it stops if evidence rules out the requested change. The goal is repeated in each
subagent brief, each PR's `## Why`, and the final report.

**Fit.** Step 1 of [Anaphor](../../anaphor/SKILL.md) builds a brief from the spec but never restates
the problem the spec solves. A restatement exposes a misread spec before implementation, which is
cheap. One caution: in reviewer briefs the restatement must not replace the accepted spec. The Spec
axis judges against requirements, and [agent handoffs](../../anaphor/references/agents.md) keep the
builder's framing away from reviewers.

**Recommendation: adapt.** Add the goal, problem, and smallest expected change to the brief and to
the PR and tour opening. If repository evidence contradicts the spec's premise, use the existing
"pause and ask the concrete question" path. Do not add a confirmation gate, and do not add the
restatement to reviewer briefs.

### ketchup, ketchup-video, poteto-help

These are chat-catch-up and help skills. Neither is relevant to delivery. `ketchup` and
`poteto-help` already existed at `ea32d95`; only `ketchup-video` is new since then.
**Recommendation: skip.**

## Adapted skills: material changes

Unless noted, the diffs compare `SKILL.md` across `e43c7ee`, `ea32d95`, and `c742dd6`. Playbook
files under `poteto-mode/playbooks/` were not diffed (**unverified**). The playbook file list is
unchanged between `ea32d95` and `c742dd6`.

### interrogate: rewritten

[Current](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/interrogate/SKILL.md),
[previous](https://github.com/cursor/plugins/blob/ea32d9562a1c9f077d7cdd3be53d07383eb18866/pstack/skills/interrogate/SKILL.md).
The skill went from 110 lines (`e43c7ee`) to 74 (`ea32d95`) to 31 (`c742dd6`). Its reference files
(`reviewer-prompt.md`, `rubric.md`, `lead-judgment.md`, `code-quality-review.md`) are gone from the
tree.

| Aspect      | 0.15.18                        | 0.15.36                               |
| ----------- | ------------------------------ | ------------------------------------- |
| Reviewers   | Read-only, one per model       | Adversaries in own worktrees          |
| Finding bar | Any reasoned finding           | A run: failing test, repro, output    |
| Excluded    | Dismissed with a reason        | Anything not run, incl. style, naming |
| Judgment    | Four lead-judgment buckets     | Coordinator reruns each command       |
| Aggregation | Cross-model agreement weighted | Union of verified findings; no voting |
| Output      | Buckets plus agreement map     | Intent, findings, dropped counts      |

The fan-out reuses arena Phase A steps 3-4 and Phase B; verification reuses arena Phase F.

**Against cross-examine.** [cross-examine](../../cross-examine/SKILL.md) still uses the four buckets
this skill dropped. [Finding requirements](../../cross-examine/references/findings.md) accept
inspection-based defects ("Code inspection can identify a defect without executing it"), and
reviewers are read-only and must _ask_ the verifier for experiments. Robustness scope adds that a
source trace can establish a security defect without running an exploit. The new upstream rule
cannot replace this wholesale:

- **Standards, Spec, Principles:** a rule breach, an unmet criterion, or a concrete maintenance cost
  is shown by inspection. Upstream now excludes exactly these ("style, naming, structure"), while
  Anaphor deliberately blocks on documented-rule violations. Keep inspection here.
- **Execution, Concurrency, Migration, Performance:** here the run rule is a real upgrade. Anaphor
  already says a speculative failure "remains unconfirmed until traced or observed". Upstream
  removes "traced" as sufficient and makes the reviewer produce the repro. Each adversary then needs
  an isolated writable worktree, which [agent handoffs](../../anaphor/references/agents.md) already
  permit ("isolated resources" with one writer each). The coordinator's independent rerun matches
  Anaphor's rule that a worker's report is a pointer, not evidence.
- **Security:** keep the trace exception. Requiring an exploit run is unsafe and unnecessary.
- **No voting:** upstream's union of verified findings agrees with Anaphor's "never turn votes into
  confidence scores". Its multi-model premise still conflicts with Anaphor's choice of one inherited
  model; perspectives come from questions, not providers.

**Recommendation: adapt for runtime passes.** For Execution, Concurrency, Migration, and
Performance, a blocking finding needs a command the coordinator reran, with its output and the
output the requirement demands. A traced-only finding is classed as consider or unresolved evidence
under robustness scope. Let those passes write repros in owned worktrees that are discarded after
the evidence is captured. Keep inspection axes and the four buckets unchanged. Record
dropped-finding counts per pass, as upstream now does. Where a formal check exists, a model
counterexample replayed against real code counts as a run.

### create-verification-skill: three additions since 0.15.9

[Current](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/create-verification-skill/SKILL.md).

1. **Launch** must reach a usable state from an empty data directory, including migrations and
   seeds. "Ready means usable, not just that a process answers"; a database health check can pass
   while init scripts still run.
2. When seed data lacks a journey's precondition, the journey **reports a failure** and the reason
   goes in `Gotchas`. The journey is never weakened.
3. A proof run on a **stand-in** (for example a container instead of a fresh VM) lists every setup
   step the stand-in performed that the real target will not. Those steps stay unverified.

**Fit.** (1) sharpens [recipe.md](../../create-feature-map/references/recipe.md)'s readiness signal
and Anaphor's readiness evidence. The empty-data-dir part belongs to project setup, so adopt the
"usable, not answering" readiness rule without moving provisioning into recipes. (2) conflicts with
[evidence.md](../../anaphor/references/verify/evidence.md), which classes missing data as a
prerequisite failure (blocked), not a product failure. Anaphor's distinction is deliberate; keep it,
and keep only the "never weaken" half, which already exists. (3) extends evidence.md's existing
"mocks and test modes require disclosed coverage limits" to whole-target substitution.

**Recommendation: adapt (1) and (3)** as one-line additions to `recipe.md` and `evidence.md`. **Skip
(2).**

### maintain-verification-skill

Byte-identical across all three revisions. **No action.**

### poteto-mode

[Current](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/poteto-mode/SKILL.md).
Material changes since 0.15.18:

- The first message restates goal, problem, and smallest change, and stops if evidence rules out the
  request (see _in-your-own-words_).
- **Fix Root Causes:** "A guard is a fix only when the state it handles is legitimate." Robustness
  scope already makes this distinction; no action.
- **Attack the Premise:** now "write the premise down and test it directly". This is a useful
  trigger to note in `implementation.md` beside `diagnosing-bugs` when two fixes fail the same gate.
  Optional.
- **Test Behavior:** now "assert what users observe" instead of literal-value assertions. Matt's
  `tdd` owns this in Anaphor; no action.
- **Model to the job:** per-spawn reasoning-level and speed tiers. Not applicable; Anaphor inherits
  the host model.
- The coordinator runs the playbook itself and never delegates the playbook to a worker. This
  matches Anaphor's coordinator ownership; no action.
- **Autopilot-stack:** "a PR stacks only on a PR it builds on." This matches Anaphor's linked PR
  dependency order; no action.

**Recommendation:** adapt the goal restatement only. Skip the rest; note the premise trigger
optionally.

### arena

[Current](https://github.com/cursor/plugins/blob/c742dd61706fbacc1b95f1a20b7b988cf096ce6c/pstack/skills/arena/SKILL.md).
From 0.15.9 to 0.15.18 the default roster dropped from three model families to two, and the phrasing
was condensed. The convergence and divergence rules and the rubric-first picking were already
present. Since 0.15.18 the changes are:

- The cross-judge must come from a family other than the parent's.
- There is longer slug-fallback and seat-drop logic, and a `composer-*` family.
- The judge may be skipped, provided the skip is reported.
- Reasoning-level selection per spawn was added.

All of this concerns model roster mechanics.
[compare-designs](../../anaphor/references/compare-designs/README.md) already discloses reduced
separation and deliberately uses one model. **Skip.**

### swarm

The diff since 0.15.18 removes an intro line and the "set N" step, and adds reasoning-level
selection. Nothing material. **Skip.**

### show-me-your-work

The only change is one line delegating the reasoning level to poteto-mode. The cross-family reviewer
requirement predates 0.15.9 and conflicts with Anaphor's one-model choice. **Skip.**

## Ranked recommendations

1. **Adapt interrogate's run rule for runtime passes** in `cross-examine`: repro-or-downgrade for
   Execution, Concurrency, Migration, and Performance; owned repro worktrees; coordinator rerun;
   dropped counts. Keep the inspection axes and the Security trace exception. Small edit, large
   evidence gain.
2. **Port maintenance rigor into `audit-feature-map`:** a per-recipe sync commit, run-as-is before
   editing, and cited evidence for intentional promise changes. Small edit; it prepares the
   formal-check branch.
3. **Add goal restatement** to Anaphor step 1 and the PR and tour opening, without a confirmation
   gate and without adding it to reviewer briefs. Trivial.
4. **Add formal-check consumption to `verify`:** rerun any project formal check whose coverage
   intersects the change, and treat a stale sync commit as stale evidence. Record model, bounds,
   tool version, and sync commit in the evidence `Target`. Moderate edit; no new tooling.
5. **Trial, then adapt `create-formal-verification-skill`** as an explicitly invoked peer to
   `create-feature-map` for one real subsystem, with the property from an accepted requirement and
   the tool provisioned by project setup. Add its maintenance branch to the audit afterwards. High
   cost; decide after the trial.
6. **Take two create-verification additions**: readiness means usable, and stand-in targets are
   disclosed. One line each.
7. **Reference `/statechart` only** for model-derived tour visuals when pstack and a provisioned
   TLA+ model already exist. Do not vendor it.
8. **Skip** `sharpen` (widens scope beyond the accepted spec), the remaining poteto-mode changes,
   arena, swarm, show-me-your-work, ketchup, ketchup-video, and poteto-help.

If adopted, update [ATTRIBUTION.md](../../anaphor/ATTRIBUTION.md) with revision `c742dd6` (0.15.36),
the interrogate rule's runtime-pass scope, and the formal-verification sources as authoring
influences rather than runtime dependencies.
