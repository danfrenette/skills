---
name: anaphor-explain-change
description:
  Create or update an evidence-linked Anaphor tour explaining a PR's value, vertical implementation
  slices, and verification. Use for standalone PR explanations or Anaphor delivery.
---

# Anaphor: explain a change

Help the owner decide whether a PR is ready to merge. Every PR delivered through Anaphor gets a
proportionate tour, including documentation and nonvisual changes. Use the same reader locally and
hosted; an inspected local preview satisfies delivery. Hosting requires an explicit request.

Read Matt Pocock's installed writing-for-agents skill before authoring. Use the project's glossary
for domain terms. If the dependency is missing, report it before drafting. Read
[content composition](references/content-composition.md) for narrative decisions and
[Anaphor integration](references/anaphor-integration.md) for local preparation, preview, updates,
and requested hosting. The app's schema and CLI help own exact fields and command syntax.

## 1. Establish the explanation and evidence

Read the accepted spec, participating PRs, pinned changes, surrounding code, decisions, and
receipts. Confirm ambiguous PR membership before including it. Record each repository's base/head
and actual tested contents using [evidence records](../anaphor-verify/references/evidence.md),
including its rules for uncommitted source and evidence applicability.

Follow [content composition](references/content-composition.md) to outline the business case and
code-led vertical slices. Pair each behavioral claim with its criterion and receipt; preserve
supplied results as supplied, with provenance. Select captures by the claim they prove using the
project's harness. Obtain required missing observations through
[anaphor-verify](../anaphor-verify/SKILL.md). A standalone tour may explain incomplete work, with
failed, blocked, unrun, or unavailable evidence visible; those gaps prevent completed factory
delivery.

**Done:** every primary slice has pinned source or an observed artifact, concise annotations, and
supporting criteria, decisions, and evidence. The main path is readable with supporting details
closed, and missing observations remain explicit.

## 2. Prepare or update the tour

Follow [prepare and persist](references/anaphor-integration.md#prepare-and-persist) to validate and
save the bundle, importing evidence before scratch/worktree cleanup. That procedure owns tour
identity, updates, storage, and revision conflicts. The tour replaces the generated Markdown
narrative and its explanation-only commit; reusable recipes stay in their owning repositories.

Keep tour revision, tested source revision, and evidence applicability separate. Preserve historical
results with their original revisions and dates; reassess them when a PR head changes.

**Done:** the valid tour and imported evidence survive worktree cleanup, participating PRs and their
dependency order are recorded, and required stale or unknown checks remain explicit.

## 3. Inspect and hand off

Follow [launch and inspect locally](references/anaphor-integration.md#launch-and-inspect-locally) in
the actual Anaphor reader. That procedure owns the content-loading checks and the boundary with
reader verification. Repair and recheck loading failures.

Return the local URL labelled for this machine, tour revision, participating PRs and source states,
key evidence, limitations, and launch/resume instructions. During factory delivery, link each PR to
its inspected tour section. When hosting is requested, follow
[publish when requested](references/anaphor-integration.md#publish-when-requested) and inspect the
hosted result before claiming delivery.

**Done:** the local preview's content, pinned code links, and assets load; during factory delivery,
every PR has its tour link. Required evidence must be passing, current, and attributable before
claiming merge readiness. Required hosting must also pass inspection. The owner makes the merge
decision.
