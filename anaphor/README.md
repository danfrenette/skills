# Anaphor

Anaphor is a draft software-delivery workflow: take an accepted spec, implement it in verifiable
increments, review it from separate perspectives, and deliver a draft PR with a linked explanation.

It is inspired by **Lauren Tan's pstack** and **Matt Pocock's skills**. Pstack informs
orchestration, competing designs, real-surface verification, and feature maps. Matt's work supplies
engineering disciplines, especially TDD and Standards/Spec review. See
[attribution and deliberate differences](ATTRIBUTION.md) for pinned sources and retained license
notices.

## Install and use

Select all eight Anaphor skills when installing from this repository. Their sibling links assume
they are installed together:

- **`anaphor`:** Coordinate an accepted spec through a draft PR and walkthrough

- **`anaphor-compare-designs`:** Settle an unresolved implementation choice with comparable
  alternatives

- **`anaphor-implement-slices`:** Execute dependent slices and verify their integration

- **`anaphor-review`:** Run Standards, Spec, and language-specific Principles agents, plus triggered
  Execution and risk passes

- **`anaphor-verify`:** Run tests and real flows; maintain affected feature recipes

- **`anaphor-create-feature-map`:** Create missing project-local recipes and prove them

- **`anaphor-audit-feature-map`:** Check an entire existing map against source and live behavior

- **`anaphor-explain-change`:** Write an evidence-linked Markdown walkthrough

Install Matt Pocock's `tdd` and `code-review` separately through your harness's skill installation
flow. Anaphor reads these installed disciplines rather than bundling copies. The Principles reviewer
combines expandable local profiles with relevant skills and primary sources, recording what it uses.
Optional references and explicit integration adaptations are documented in
[dependencies](references/dependencies.md).

For development in this source repository, the root
[maintenance setup](../README.md#maintaining-this-repository) restores the external skills from the
generated project lock. That lock does not create transitive installs for users of the family.

The initial [Principles profiles](../anaphor-review/references/principles/README.md) cover
Ruby/Rails through thoughtbot and Sandi Metz, JavaScript/TypeScript through Kent C. Dodds and Matt
Pocock, and frontend concerns through Vercel. Add concrete checks, examples, exceptions, and sources
within those profiles; the coordinator does not need another phase for each language.

Invoke `anaphor` with the accepted spec and working repository or repositories. Include the testing
decisions already confirmed during `to-spec`. The coordinator is intended for explicit invocation;
the other skills have descriptions so the coordinator and users can reach them independently.
Harness support for invocation metadata varies; explicit invocation remains the portable entry
point.

The factory uses the host's agent, Git, execution, and browser interfaces. One model is sufficient.
Parallel capacity is optional; fresh contexts preserve role separation when work runs sequentially.

## Project integration

Project instructions should point to their own setup and verification procedures. Anaphor can use a
supplied environment without knowing how it was provisioned. It does not require a particular issue
tracker, database, package manager, or directory topology.

Keep feature maps in their owning repositories. Extend existing maps and harnesses. If a map is
missing, create coverage for the affected feature and execute that recipe; whole-app audits are an
explicit separate operation.

Anaphor stops on unresolved required verification prerequisites after one safe documented recovery
attempt. Product failures return to implementation. Successful delivery ends at draft PRs and a
linked walkthrough; readiness, merge, and deployment remain subsequent decisions.

## Draft status

These files are an initial draft, not a proven automation. Structural checks and scenario
walkthroughs are recorded in [validation notes](VALIDATION.md). Live trials must establish that the
instructions produce the intended behavior before treating the workflow as validated.
