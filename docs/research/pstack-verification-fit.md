# pstack verification skills in Anaphor

Research date: 2026-10-11. Anaphor baseline: `f6571f62d5cbaa655bc4b8e61d33cabfbea09691`. This is an
integration assessment, not an implemented workflow change or a live reliability trial.

## Finding

The two skills belong to the factory's **project verification infrastructure**: create it when a
project is onboarded, consume it during delivery, and maintain it between delivery runs. Anaphor
already implements most of their mechanics. The useful next work is to make onboarding and
maintenance explicit, preserving the stronger delivery proof requirements already in Anaphor.

Lauren Tan's [July 30 post](https://x.com/poteto/status/2082874054483255805) names exactly
`create-verification-skill` and `maintain-verification-skill`. It describes verification as team
infrastructure and recommends daily maintenance through Cursor cloud agents. The post was read in
the browser after the web fetch returned 403; its two GitHub links establish the research scope.

The inspected upstream revision is `ea32d9562a1c9f077d7cdd3be53d07383eb18866`, whose
[pstack manifest](https://github.com/cursor/plugins/blob/ea32d9562a1c9f077d7cdd3be53d07383eb18866/pstack/.cursor-plugin/plugin.json)
reports version 0.15.18. Both skill files are byte-identical to revision
`e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a`, already recorded in Anaphor's
[attribution](../../skills/software-factory/anaphor/ATTRIBUTION.md). These are existing design
sources, not newly introduced upstream capabilities.

## What the upstream skills do

- **Creation:** Inspect the repository's user surface, startup, harness, evidence, and isolation;
  generate `.cursor/skills/verify-<app>/SKILL.md` with launch, doctor, drive, evidence, and cleanup
  instructions. Seed roughly three to five identifiable features. Execute the generated guide with
  one mapped feature before delivery. It can fix startup or use limited cleanup-owned scaffolding.
  [Pinned creation source](https://github.com/cursor/plugins/blob/ea32d9562a1c9f077d7cdd3be53d07383eb18866/pstack/skills/create-verification-skill/SKILL.md).
- **Maintenance:** Inspect every feature with read-only source workers, reconcile their recipes,
  inspect recent churn for missing surfaces, and let one owner drive every feature live. Limit edits
  to the verification directory and owned helpers. Distinguish documentation drift, harness gaps,
  and product regressions. Return clean, changed, or blocked; publish at most one corrections PR.
  Keep run notes in scratch. Explicitly unreachable features need the prerequisite and attempted
  route recorded.
  [Pinned maintenance source](https://github.com/cursor/plugins/blob/ea32d9562a1c9f077d7cdd3be53d07383eb18866/pstack/skills/maintain-verification-skill/SKILL.md).

The feature map is executable navigation knowledge, not a list of product promises. Its
[example index](https://github.com/cursor/plugins/blob/ea32d9562a1c9f077d7cdd3be53d07383eb18866/pstack/skills/create-verification-skill/references/feature-map-example/README.md)
separates feature files and user entry points. Recipes and per-run proof are different artifacts:
the recipe persists as infrastructure; a receipt establishes what actually ran on a given revision.

## Where they fit today

| Responsibility                 | Anaphor owner                 | Fit            |
| ------------------------------ | ----------------------------- | -------------- |
| Project bootstrap              | Project setup; map creation   | Partial        |
| Changed-feature recipes        | `anaphor-create-feature-map`  | Covered        |
| Acceptance flows               | `anaphor-verify`              | Covered        |
| Full-map audit                 | `anaphor-audit-feature-map`   | Mostly covered |
| Project records                | `anaphor-reconcile`           | Adjacent       |
| Scheduled maintenance delivery | Project periodic instructions | Not defined    |

**Creation overlaps with a narrower Anaphor operation.**
[anaphor-create-feature-map](../../skills/software-factory/anaphor-create-feature-map/SKILL.md)
already generates an app guide, index, and recipes when needed. It respects the project's discovery
convention and falls back to `docs/verification/`, rather than requiring Cursor. Automatic creation
covers only the affected feature and executes every new or changed recipe. Upstream's initial
feature sample and one-feature smoke proof are useful bootstrap behavior, but insufficient to
certify all those recipes under Anaphor's existing contract.

**Maintenance substantially overlaps with the existing audit.**
[anaphor-audit-feature-map](../../skills/software-factory/anaphor-audit-feature-map/SKILL.md)
already compares the index and all recipes against source, checks recent changes, drives the map,
repairs drift, reports regressions, and preserves evidence through cleanup. It permits read-only
source workers and keeps a single owner for shared app state. It does not prescribe one worker per
feature, a scheduler contract, or clean/changed/blocked PR publication behavior. Those are concrete
integration choices, not reasons to duplicate the audit engine.

**Verification remains a delivery gate.**
[anaphor-verify](../../skills/software-factory/anaphor-verify/SKILL.md) selects affected criteria,
routes, and roles; proves visible and persisted effects; and binds results to tested contents. Its
[blocker procedure](../../skills/software-factory/anaphor-verify/references/evidence.md) stops
delivery after one documented safe recovery fails. A maintenance report can be complete with
coverage gaps. Anaphor delivery still requires every required criterion to pass. Upstream's
unreachable-feature label must never become a functional pass.

**Reconciliation has a different owner.**
[anaphor-reconcile](../../skills/software-factory/anaphor-reconcile/SKILL.md) updates authoritative
project records from decisions and receipts. Verification owns live recipe proof. A periodic map
audit should invoke reconciliation only when an affected record needs it, rather than absorbing
general documentation upkeep into verification maintenance.

## Recommended integration

### 1. Add an explicit onboarding path

Extend `anaphor-create-feature-map` with an explicitly requested project-bootstrap branch, disclosed
in a reference if needed. Keep ordinary spec-driven creation scoped to affected behavior.

Bootstrap should discover the primary surfaces, reuse project-owned setup, generate a small useful
initial map, label its coverage limits, and execute every recipe it presents as proven. This also
resolves the current awkward case where auditing a project with no map routes to a creator that
expects an affected feature. Start with this existing owner; a separate skill earns its place only
if actual use needs an independent invocation and completion contract.

Completion: a fresh agent can find the guide, launch the documented target, run doctor, execute each
seeded recipe, capture proof, and clean up while retaining evidence. Missing access or startup
remains a named setup dependency. Provisioning continues to belong to the project.

### 2. Give the audit a maintenance publication contract

Keep `anaphor-audit-feature-map` as the engine. Add a maintenance reference covering the named
target, allowed edit scope, complete coverage accounting, and outcomes:

- **Clean:** complete source/live coverage; no changes and no PR.
- **Changed:** proven verification-document or owned-helper corrections; at most one draft PR.
- **Blocked:** incomplete required coverage or corrections that cannot be proven/published; report
  the prerequisite and retained evidence.
- **Product failure:** report the actual defect with its intended assertion and proof. Keep product
  fixes outside the maintenance PR; resolve them through an accepted delivery task.

Use independent source workers when they help and capacity exists, retaining Anaphor's sequential
fallback. One live driver owns shared state. Re-drive changed recipes and helpers before
publication. Draft PRs preserve Anaphor's existing publication boundary; upstream's unspecified PR
readiness is not a reason to change it.

### 3. Attach scheduling to project instructions

[periodic-work](../../periodic-work/SKILL.md) already dispatches project-owned `DAILY.md`,
`WEEKLY.md`, or `MONTHLY.md`. A project can point those instructions at its verification guide and
the audit's maintenance contract. Scheduling belongs to the host, which owns recurrence and
overlapping runs. Explicitly identify the checkout, target, access, allowed writes, PR publication
authorization, and notification behavior before unattended use.

Choose cadence from observed churn and execution cost. The post's daily recommendation is a useful
option; the current creation skill says to suggest cadence only when asked. This research does not
create an automation. Maintenance examines application verification assets, distinct from an
upstream skill-update loop that this repository deliberately does not maintain.

### 4. Validate on one real project before widening adoption

Run a bootstrap trial, an unchanged maintenance trial, a selector-drift trial, and a
product-regression trial. Confirm that clean runs avoid PRs, corrections are live-proven,
regressions preserve intended assertions, blocked access stays explicit, and proof survives cleanup.
Measure run duration and recovery effort to choose cadence. Static instruction review cannot
establish agent reliability.

## Decision

Adopt the lifecycle through the existing creation, audit, verification, and periodic-work owners.
Prioritize explicit bootstrap scope and the maintenance publication contract. Preserve project-owned
setup, host-independent locations, every-changed-recipe proof, revision-bound delivery evidence, and
draft-only publication. Installing two overlapping runtime dependencies or adding a full-map audit
to every spec run would not address the identified gaps.

Only this research document was added. Skills, dependencies, schedules, and upstream attribution
remain unchanged.
