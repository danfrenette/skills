---
name: anaphor
description:
  Deliver an accepted product spec as verified implementation, a draft PR, and a linked walkthrough.
disable-model-invocation: true
---

# Anaphor

Own an accepted spec through implementation, verification, and a draft PR. Start after product
discovery; an accepted spec from Matt Pocock's `to-spec` is the expected input. Its product
synthesis and ticket-publication workflow stays upstream.

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

## 4. Reconcile project records

Use [anaphor-reconcile](../anaphor-reconcile/SKILL.md) after integrated verification to update
affected product, domain, setup, and tracker records. Link the existing spec and receipts; keep
accepted intent separate from verified and deployed behavior. Review the documentation diff.
Changes to executable instructions or recipes return to affected review and verification.

**Done:** each affected authoritative record is updated, unchanged with a reason, or explicitly
blocked. A required unresolved record keeps delivery open.

## 5. Deliver

Push the verified branches and open draft PRs with the spec, scope, outcome, and verification
evidence. Required blocked or unrun checks prevent this step. Link participating PRs and explain
their dependency order. Reuse existing PRs if publication is interrupted.

Use [anaphor-explain-change](../anaphor-explain-change/SKILL.md) to publish a durable walkthrough
and link it from each PR. Review its final diff and links. For explanation-only commits, preserve
the earlier test provenance and explain why it still applies; executable, configuration, or recipe
changes return to affected review and verification. Confirm final heads and draft status. Report the
PRs, walkthrough, implementation and final revisions, evidence, and limitations. Readiness, merge,
and deployment remain separate user decisions. Reconcile affected delivery links and status after
publication; opening a draft PR does not establish deployed behavior.

**Done:** the delivered revision is accounted for by review and verification, and every
participating draft PR links the explanation. An unfinished required check or unpublished
walkthrough keeps delivery open.

## Continue in a fresh session

When the user requests a session handoff, read Matt Pocock's installed `handoff` skill and use it to
prepare the continuation document. Follow its temporary-file location and artifact-reference rules;
point to the implementation brief, current revisions, verification receipts, remaining work, and the
next applicable Anaphor skill. The continuation document does not satisfy draft-PR delivery or
replace the published walkthrough.
