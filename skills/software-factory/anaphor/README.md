# Anaphor

Anaphor is a software-delivery workflow: take an accepted spec, implement it in verifiable
increments, review it from separate perspectives, and deliver a draft PR with an inspected local
tour.

It is inspired by **Lauren Tan's pstack** and **Matt Pocock's skills**. Pstack informs
orchestration, competing designs, real-surface verification, and feature maps. Matt's work supplies
engineering disciplines, especially TDD and Standards/Spec review. See
[attribution and deliberate differences](ATTRIBUTION.md) for pinned sources and retained license
notices.

## Install and use

Select all nine Anaphor skills when installing from this repository. Their sibling links assume they
are installed together:

- **`anaphor`:** Coordinate an accepted spec through draft PRs and inspected tours

- **`anaphor-compare-designs`:** Settle an unresolved implementation choice with comparable
  alternatives

- **`anaphor-implement-slices`:** Execute dependent slices and verify their integration

- **`anaphor-review`:** Run Standards, Spec, and language-specific Principles agents, plus triggered
  Execution and risk passes

- **`anaphor-verify`:** Run tests and real flows; maintain affected feature recipes

- **`anaphor-create-feature-map`:** Create missing project-local recipes and prove them for affected
  behavior or explicitly requested project bootstrap

- **`anaphor-audit-feature-map`:** Check an entire existing map against source and live behavior and
  publish proven corrections when maintenance is requested

- **`anaphor-explain-change`:** Create or update an evidence-linked local Anaphor tour

- **`anaphor-reconcile`:** Update affected product, domain, setup, and tracker records

Install Matt Pocock's `tdd`, `code-review`, and `writing-for-agents` through your harness's skill
installation flow; add `domain-modeling` for terminology/decision reconciliation and `handoff` for
user-requested session continuations. Resolve sibling skills relative to the installed family
directory. If a required skill is missing, name it and its role and leave the dependent step
incomplete. Installation is a separate action.

Check authorship when another library exposes the same skill name. Record the installed source used
for a run and surface material instruction conflicts. Integration adaptations live at their points
of use: [implementation](references/implementation.md), [review](../anaphor-review/SKILL.md), and
the coordinator's continuation branch. Optional source triggers live in the affected procedure and
Principles profiles; load them only when that branch is reached.

For development in this source repository, the root
[dependency setup](../../../README.md#project-dependencies) restores the external skills from the
generated project lock. That lock does not create transitive installs for users of the family.

The [Principles profiles](../anaphor-review/references/principles/README.md) cover Ruby/Rails
through thoughtbot and Sandi Metz, JavaScript/TypeScript through Kent C. Dodds and Matt Pocock, and
frontend concerns through Vercel. Add concrete checks, examples, exceptions, and sources within
those profiles; the coordinator does not need another phase for each language.

Invoke `anaphor` with the accepted spec and working repository or repositories. Include the testing
decisions already confirmed during `to-spec`. The coordinator is intended for explicit invocation;
the other skills have descriptions so the coordinator and users can reach them independently.
Harness support for invocation metadata varies; explicit invocation remains the portable entry
point.

The factory uses the host's agent, Git, execution, and browser interfaces. One model is sufficient.
Parallel capacity is optional; fresh contexts preserve role separation when work runs sequentially.

## Project integration

Project instructions should point to their own setup and verification procedures. Anaphor can use a
supplied environment without knowing how it was provisioned. Its implementation brief checks the
project's readiness evidence against the accepted spec before implementation begins. It does not
require a particular issue tracker, database, package manager, or directory topology.

Start with the project's setup procedure for workspace readiness, then use Matt Pocock's
product-decision skills to establish the accepted spec and testing decisions. Hand that spec and the
ready workspace to Anaphor. Any prerequisites introduced during product decisions return to the
workspace setup owner before implementation.

Anaphor reuses the project's authentication preflight and the owning app's verification map.
Generated recipes retain the project's harness and link its authentication procedure; when no
browser tool is designated, agent-browser is the default. Launch, doctor, drive, evidence, and
cleanup remain the shared recipe structure, and every new or changed recipe must be executed
successfully.

Keep feature maps in their owning repositories. Extend existing maps and harnesses. If a map is
missing, create coverage for the affected feature and execute that recipe; whole-app audits are an
explicit separate operation.

For project onboarding, request the creation skill's
[bootstrap branch](../anaphor-create-feature-map/references/bootstrap.md). For periodic upkeep,
request the audit skill's
[maintenance branch](../anaphor-audit-feature-map/references/maintenance.md) with its named target
and publication authorization. Project periodic instructions and the host scheduler own recurrence
and shared-resource overlap; these branches add no phase to ordinary spec delivery.

Anaphor stops on unresolved required verification prerequisites after one safe documented recovery
attempt. Product failures return to implementation. Successful delivery ends at draft PRs and a
linked, inspected tour for every PR; readiness, merge, and deployment remain subsequent decisions.
The local Anaphor app uses the hosted reader without authentication or publication. Persistent
tours, captures, and receipts live outside product repositories; recipes stay alongside code. Local
URLs serve review on the current machine. Publish the same tour only when requested for sharing,
with appropriate owner access. See the explanation skill's
[integration reference](../anaphor-explain-change/references/anaphor-integration.md) for
preparation, revision freshness, local inspection, and requested hosting.

## Validation scope

Structural checks have passed; end-to-end reliability has not yet been established through live
implementation trials. Each change's verification evidence belongs in its PR. The root
[usage guide](../../../README.md#anaphor) describes installation, invocation, and the delivery
lifecycle.
