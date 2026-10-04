# Anaphor: agreed workflow

Agreed 2026-10-04. This brief records the decisions from the design discussion; it is not an
installed skill. The executable draft starts at [anaphor](../anaphor/SKILL.md). Source attribution and
pinned upstream references are in [the attribution note](../anaphor/ATTRIBUTION.md).

## Entry and ownership

Start from an accepted product spec produced by Matt Pocock's `to-spec`, including its acceptance
criteria and confirmed test boundaries. The factory owns implementation through verified delivery.
Product discovery and upfront product planning precede this workflow.

Inspect the affected code, resolve implementation details, and split larger work into verifiable
slices. If implementation exposes an unresolved product decision, pause the affected work and
present the concrete decision to the user. Independent work may continue.

## Workspace boundary

Workspace provisioning stays in project-local instructions or a workspace skill. That procedure owns
environment creation, credentials, database provisioning, and infrastructure recovery.

Execution and verification use the supplied checkout and the project's documented commands, targets,
access prerequisites, and readiness checks. They may start and check the services needed for the
task. They refer setup failures back to the project procedure rather than incorporating its
provisioning details.

## Implementation and orchestration

Use Matt's TDD workflow for implementation. Carry confirmed test boundaries from the accepted spec
into each implementation slice; request confirmation only when they are missing or materially
change.

The coordinator owns acceptance criteria, dependencies, integration, and the evidence supporting
completion. Give workers bounded tasks and explicit ownership. Keep one writer per shared checkout
or mutable resource. Inspect returned changes and evidence before accepting a worker's completion
claim.

Use the inherited model by default. Distinct perspectives come from different questions, source
material, and fresh contexts. Limited concurrency permits sequential fresh-context work. If only one
context is available, report that reduced separation instead of describing successive passes as
independent reviewers. Model agreement is not verification evidence.

## Review

Use Matt's `code-review` Standards and Spec axes as the baseline, preserving the distinction between
documented rule violations and requirements failures.

Add a third, independent **Principles** subagent for language/framework design, testing, and idioms.
Start with thoughtbot and Sandi Metz for Ruby/Rails, Kent C. Dodds and Matt Pocock for
JavaScript/TypeScript, and Vercel guidance for frontend work. Maintain expandable local profiles
that combine concrete checks with relevant skill and primary-source references. Report Principles
separately from Standards and Spec; heuristics become mandatory only when adopted by the project.

Add a fresh Execution review for substantive behavior changes. Trigger specialized review for
affected concerns such as authorization, concurrency, migrations, or performance. Reviewers receive
the requirements, applicable rules, and pinned changes; initially omit the builder's persuasive
rationale and other reviewers' conclusions.

Evaluate findings against reachable behavior and source evidence. Resolve actionable findings and
repeat the affected checks. More favorable reviews do not outweigh a reproduced failure.

## Verification and feature maps

Use the repository's tests and existing driving harness. Exercise browser-visible behavior with
agent-browser or Playwright as appropriate to the available harness. Verify the expected visible
outcome, relevant persisted effects, and meaningful failure paths.

Read the relevant feature-map entries before implementation. Update affected entries, add recipes
for new behavior, and remove obsolete instructions. Execute changed recipes before calling them
verified.

When the repository has no feature map, create and prove the affected feature's recipe
automatically. Broader feature discovery and full-map audits remain separate operations. Do not
imply that an unexecuted recipe was verified because a neighboring recipe passed.

Associate verification evidence with the actual delivered revision. After fixes or integration,
rerun affected checks. For uncommitted work, HEAD alone does not identify the tested changes; retain
the corresponding change identity as well.

Keep completion evidence concise: criterion, action, expected result, observed result, evidence
location, and revision. Report pass, fail, blocked, or not run explicitly.

## Failed checks and blockers

A product failure observed through a working test or browser harness returns to implementation for
repair.

A required browser check is blocked when a necessary target, credential, service, data prerequisite,
or tool cannot be reached through the documented execution procedure. Allow one relevant, safe
recovery attempt, such as restarting an owned dev server or repairing a stale selector for working
behavior. Recovery must preserve the behavior being asserted.

If the prerequisite remains unavailable, stop and report the failed prerequisite, attempted
recovery, unverified acceptance criteria, and the input or repair needed to resume. Required
verification must succeed before draft PR creation.

## Delivery

After implementation, review, required verification, and affected feature-map updates are complete,
open a draft PR. Leave it in draft status for the user.

Then produce a durable Markdown walkthrough and link it from the PR. Explain the user-visible
behavior, domain decisions, important code paths, and verification evidence. Add diagrams or
recordings when they clarify the change. Interactive or hosted Tours are optional extensions.

The successful endpoint is the draft PR with its linked explanation. Marking it ready, merging, and
deployment are outside that endpoint.

## Skill composition and naming

Adopt Matt's TDD and code-review workflows within this orchestration. Reference other reusable
disciplines only when their branches apply, including design comparison, diagnosis, domain modeling,
and prototypes. Preserve their meaningful prerequisites; make adaptations explicit rather than
silently dropping rules.

Use pstack as architectural guidance for orchestration, review depth, verification, and feature
maps. The decisions above deliberately establish our own behavior where upstream differs, including
same-model perspectives, required affected-map maintenance, and draft PR delivery.

The collection and coordinator use **Anaphor**; supporting skills use the `anaphor-` prefix. Credit
pstack and Matt Pocock openly in the family documentation and preserve source provenance.
