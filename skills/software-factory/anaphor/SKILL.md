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

Read the accepted spec, testing decisions, repository instructions, and affected feature-map
entries. Inspect local changes before choosing the baseline, then create one brief containing:

- Spec source and observable criteria, preserving requirement identifiers or assigning stable ones.
- Confirmed test boundaries and each criterion's owning surface and verification route.
- Owning repositories, original baseline commits, working paths, and local changes to preserve.
- Setup and verification pointers, runtime targets, resource ownership, and readiness evidence.
- User- or project-supplied verification and tour procedures, including their completion
  requirements.

Reuse the supplied checkout and environment when they meet the task's needs. Compare the project's
setup handoff with the spec's required services, access, data, and tools. Reuse applicable readiness
evidence; run documented launch and readiness checks for missing or changed prerequisites before
implementation or worker dispatch. Product decisions may add prerequisites after setup. Return
missing provisioning to the setup owner and keep dependent implementation blocked until readiness
passes. Readiness proves access to the environment; verification proves the criteria.

Keep exploratory research in scratch files or linked workspace resources; put useful rationale and
source links in the PR description. Commit research documents only when explicitly requested.
Durable product/API documentation and recipes follow their repository publication rules. Tour
storage follows the selected delivery procedure.

Resolve code-level choices from the spec and repository evidence. When a choice changes product
behavior beyond those decisions, pause the affected work and ask the user the concrete question.
Continue independent work while that answer is pending.

For robustness proposals during implementation or review, apply
[robustness scope](references/robustness-scope.md). Record accepted expansions and deferrals in the
brief; carry them through slice criteria and worker handoffs so speculative protection does not
become an implicit delivery requirement.

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

Use [anaphor-reconcile](../anaphor-reconcile/SKILL.md) after integrated verification. It owns record
selection, evidence classification, and documentation checks. Return executable, configuration, or
recipe changes to affected review and verification.

**Done:** every affected authoritative record is updated or unchanged with a reason; required
blocked records keep delivery open.

## 5. Deliver

Push the verified branches and open draft PRs with the spec, scope, outcome, and verification
evidence. Required blocked or unrun checks prevent this step. Link participating PRs and explain
their dependency order. Reuse existing PRs if publication is interrupted.

Create or update the tour for every PR, including small and nonvisual changes:

- If the user or project supplies a tour procedure, follow it through inspection and its required
  delivery steps, including publication approvals.
- Otherwise, use [anaphor-explain-change](../anaphor-explain-change/SKILL.md). Open and inspect the
  local Anaphor reader and link its relevant section from each PR. An inspected local preview
  satisfies tour delivery without authentication or publication. Publish the same content and media
  only when explicitly requested.

For the default tour, the explanation skill owns storage, provenance, inspection, PR links, and
requested hosting. Apply the selected procedure's corresponding requirements for a supplied tour.
Source changes after verification follow
[evidence applicability](../anaphor-verify/references/evidence.md#evidence-applicability). Return
executable, configuration, or recipe changes to affected review and verification.

Confirm final heads and draft status, then reconcile affected delivery links and status. Report PRs,
tour URL and revision, delivered and tested source states, evidence, limitations, and tour access or
resume instructions. Merge and deployment remain separate user decisions.

**Done:** every participating draft PR links an inspected tour, review and verification cover its
final source state, and the selected tour procedure is complete. Missing, failed, blocked, unrun,
stale, or unknown required evidence keeps delivery incomplete, as does required publication or
approval still pending.

## Continue in a fresh session

When the user requests a session handoff, read Matt Pocock's installed `handoff` skill and use it to
prepare the continuation document. Follow its temporary-file location and artifact-reference rules;
point to the implementation brief, current revisions, verification receipts, remaining work, and the
next applicable Anaphor skill. The continuation document does not satisfy draft-PR delivery or
replace the inspected PR tour.
