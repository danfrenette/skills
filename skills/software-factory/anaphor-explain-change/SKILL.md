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

Read the accepted spec, participating PRs and pinned changes, surrounding code, decisions, and
verification receipts. Identify each repository's delivered base/head and actual tested source
state. For uncommitted runs, retain the patch and relevant untracked contents or hashes; HEAD alone
cannot describe what ran. Confirm ambiguous PR membership before including it.

Plan a problem/value opening and the primary vertical slices. Follow each slice from its entry point
through consequential responsibilities and decisions to its observable outcome and failure behavior.
Link source at pinned revisions and explain why each selected location matters. Cover
cross-repository dependencies and rollback constraints where relevant.

Keep verification beside the slice it supports: spec criterion, action, expected and observed
outcomes, recorded result, target/build, role/data context, tested source state, and limits. Use
screenshots for useful visible states, videos for behavior involving interaction or time, and
command/API evidence for nonvisual changes. Follow the project's capture harness; agent-browser is
the default when none is designated. Captures and illustrative diagrams have distinct purposes.

Obtain required missing verification through [anaphor-verify](../anaphor-verify/SKILL.md). Preserve
supplied results as supplied, with their provenance. Standalone explanation of incomplete work may
show failed, blocked, unrun, or unavailable evidence; required gaps prevent completed factory
delivery and a merge-ready claim.

**Done:** each primary slice has a narrative and linked criteria, source, decisions, and evidence;
missing observations and rationale remain explicit.

## 2. Prepare or update the tour

Use the integration reference to create or update a validated bundle in the persistent Anaphor
workspace outside product repositories. Import captures, receipts, and source-state evidence before
scratch/worktree cleanup. Keep reusable recipes in their owning repositories and historical
walkthroughs readable. The tour replaces the generated Markdown narrative and its explanation-only
commit.

Reuse the logical tour and stable section/evidence identifiers. A shared tour records every PR and
dependency order; each PR links its relevant section. Preserve old results with their original
tested revisions and dates. A new PR head makes older evidence stale by default. Retaining
applicability requires an inspected-delta rationale while preserving the original run; a rerun
creates a new record. Tour revision, tested source revision, and applicability are separate facts.

**Done:** the valid tour and referenced evidence survive implementation worktree cleanup, revisions
are accounted for, and stale or unknown required checks are explicit.

## 3. Inspect and hand off

Open the actual local Anaphor preview. Check section navigation and anchors, text, pinned source
links, media playback/accessibility, receipt access, and evidence freshness against every delivered
source state. Repair and recheck failures. Preserve the final inspection receipt outside the tour
when embedding it would require inspecting another new revision.

Return the local preview URL labelled for this machine, tour revision, participating PRs and source
states, key evidence, and remaining limitations. Link the tour from every participating PR during
factory delivery. A local URL serves solo review; external readers need a hosted URL and access.
When hosting is requested, publish the same content and assets, preserve recovery metadata, and
inspect authenticated hosted reading before claiming hosted delivery.

**Done:** the real reader and evidence links have been inspected and every participating PR has its
tour link. Broken previews, invalid provenance, and unresolved required evidence leave factory
delivery incomplete. Missing, failed, blocked, unrun, stale, or unknown required evidence prevents a
merge-ready claim. The owner makes the merge decision; publication, merge, and deployment remain
separate actions.
