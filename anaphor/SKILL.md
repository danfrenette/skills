---
name: anaphor
description:
  Deliver an accepted product spec as verified implementation, a draft PR, and a linked walkthrough.
disable-model-invocation: true
---

# Anaphor

Own an accepted spec through implementation, verification, and a draft PR. Start after product
discovery; a spec from Matt Pocock's `to-spec` is the expected input. Read
[dependencies](references/dependencies.md) before dispatching work.

## 1. Establish the implementation brief

Read the accepted spec, testing decisions, applicable repository instructions, and affected
feature-map entries. Record the spec source, observable criteria, confirmed test boundaries, owning
repositories, baseline commits, working paths, and setup/verification pointers in one brief.
Preserve the spec's requirement identifiers, or assign stable identifiers when absent.

Inspect local changes before choosing the working baseline. Reuse the supplied checkout and
environment when they meet the task's needs. Provisioning belongs to the project's setup procedure;
execution may run documented launch and readiness checks. Report unavailable prerequisites instead
of inventing infrastructure.

Resolve code-level choices from the spec and repository evidence. When a choice changes product
behavior beyond those decisions, pause the affected work and ask the user the concrete question.
Continue independent work while that answer is pending.

**Done:** every criterion has an owning surface and verification route; the baseline and confirmed
test boundaries are known. Missing product decisions remain explicit dependencies.

## 2. Execute

Choose the smallest applicable path:

- One verifiable change: follow [implementation](references/implementation.md).
- Multiple independently verifiable changes: use
  [anaphor-implement-slices](../anaphor-implement-slices/SKILL.md).
- An unresolved implementation choice has competing interfaces, ownership models, or failure
  behavior: use [anaphor-compare-designs](../anaphor-compare-designs/SKILL.md) for that choice, then
  resume implementation. Keep accepted product decisions fixed.

For delegated work, read [agent handoffs](references/agents.md). Keep ownership, dependencies, and
observed results in the brief. A worker's completion message is a pointer to inspect its changes and
evidence.

**Done:** every criterion is implemented, and each changed behavior has a passing executed
verification recipe. A required verification blocker stops the run under
[anaphor-verify](../anaphor-verify/SKILL.md).

## 3. Integrate and review

Inspect the complete change from the original baseline in every owning repository with
[anaphor-review](../anaphor-review/SKILL.md). Resolve actionable findings, then use
[anaphor-verify](../anaphor-verify/SKILL.md) on the integrated result. Checks already run on that
exact result may be reused with their provenance; rerun checks affected by fixes or integration.

**Done:** every criterion passes, affected feature maps are current and live-proven, required
repository checks pass, and all triggered review passes are assessed with no unresolved blocking
finding.

## 4. Deliver

Follow [draft PR handoff](references/handoff.md): open a draft PR, then publish and link a durable
Markdown walkthrough. Keep the PR in draft status for the user. Report the PR, walkthrough, tested
revision, evidence, and any limitations.

**Done:** the delivered revision is accounted for by review and verification, and every
participating draft PR links the explanation. An unfinished required check or unpublished
walkthrough keeps delivery open.
