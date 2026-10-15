---
name: anaphor
description:
  Deliver an accepted product spec as verified implementation, a draft PR, and an inspected local
  tour.
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

Keep exploratory research and comparison notes in scratch files or linked workspace/project
resources. Put useful rationale and source links in the PR description; commit research documents
only when the user explicitly requests them. Durable product/API documentation and verification
recipes retain their repository publication rules. Per-PR tours and evidence use persistent Anaphor
storage outside product repositories.

Inspect local changes before choosing the working baseline. Reuse the supplied checkout and
environment when they meet the task's needs. Read the project's setup handoff and confirm its
readiness evidence covers the accepted spec's required services, access, data, and test tools.
Record working paths and revisions, runtime targets, resource ownership, observed checks, and
evidence pointers in the brief. Reuse applicable evidence; run the documented launch and readiness
checks for missing or changed prerequisites before starting implementation or dispatching workers.
Readiness establishes a usable environment; criterion verification still follows implementation.

Provisioning belongs to the project's setup procedure. Return missing infrastructure, credentials,
or data provisioning to that owner and keep implementation blocked until the required readiness
checks pass. Product decisions made after setup may introduce new prerequisites; check those against
the accepted spec rather than treating an earlier setup result as sufficient for every task.

Resolve code-level choices from the spec and repository evidence. When a choice changes product
behavior beyond those decisions, pause the affected work and ask the user the concrete question.
Continue independent work while that answer is pending.

**Done:** every criterion has an owning surface and verification route; the baseline and confirmed
test boundaries are known, and required workspace readiness has observed evidence. Missing product
decisions remain explicit dependencies.

## 2. Execute

When implementation or prototyping uses a supplied visual reference, first follow
[reference inspection](references/visual-references.md).

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
accepted intent separate from verified and deployed behavior. Review the documentation diff. Changes
to executable instructions or recipes return to affected review and verification.

**Done:** each affected authoritative record is updated, unchanged with a reason, or explicitly
blocked. A required unresolved record keeps delivery open.

## 5. Deliver

Push the verified branches and open draft PRs with the spec, scope, outcome, and verification
evidence. Required blocked or unrun checks prevent this step. Link participating PRs and explain
their dependency order. Reuse existing PRs if publication is interrupted.

Use [anaphor-explain-change](../anaphor-explain-change/SKILL.md) to create or update the tour for
every PR, including small and nonvisual changes. Open and inspect the local Anaphor reader and link
its relevant section from each PR. A coordinated tour records every participating PR, dependency
order, and source state. Label local links for the current machine; external readers need requested
hosting and access. An inspected local preview satisfies tour delivery without authentication or
publication. Publish the same content and media only when explicitly requested.

Keep recipes in their repositories and tours, captures, and receipts in persistent storage outside
implementation worktrees. Preserve historical walkthroughs; new delivery requires no second Markdown
narrative or explanation-only commit. Source changes after verification require an applicability
assessment or rerun while retaining the original tested revisions; executable, configuration, or
recipe changes return to affected review and verification.

Confirm final heads and draft status. Report PRs, tour URL and revision, implementation and final
source states, evidence, limitations, and how to resume the local reader. Reconcile affected
delivery links and status. Opening a draft PR, inspecting a tour, declaring merge readiness,
merging, and deploying remain distinct actions and user decisions.

**Done:** the delivered source states are accounted for by review and verification, and every
participating draft PR links an inspected tour. Broken previews, invalid provenance, or missing,
failed, blocked, unrun, stale, or unknown required evidence leave delivery incomplete. Hosting is
required only when requested.

## Continue in a fresh session

When the user requests a session handoff, read Matt Pocock's installed `handoff` skill and use it to
prepare the continuation document. Follow its temporary-file location and artifact-reference rules;
point to the implementation brief, current revisions, verification receipts, remaining work, and the
next applicable Anaphor skill. The continuation document does not satisfy draft-PR delivery or
replace the inspected PR tour.
