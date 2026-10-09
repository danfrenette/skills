---
name: anaphor-implement-slices
description:
  Implement an accepted spec as dependent, verifiable slices when one change spans multiple
  independently reviewable behaviors.
---

# Anaphor: implement slices

Own the integration branch, requirement coverage, and the next ready slice. Read
[agent handoffs](../anaphor/references/agents.md). A slice graph organizes execution of the accepted
spec; product discovery remains upstream.

## Form the graph

1. Read the implementation brief, complete spec, and confirmed testing decisions. Record the
   starting revision of each affected repository.
2. Reuse supplied tickets and blocking relationships, reconciling them with the accepted spec. Fill
   coverage gaps with narrow slices that deliver observable behavior through the necessary layers.
   For each, record its criteria, verification recipe, owning repositories, write scope, and genuine
   blockers. Assign every requirement to a slice; distinguish prerequisites from preferred ordering.
3. Put a necessary behavior-preserving preparation first. For migrations that cannot land in
   vertical slices, use compatible expansion, caller migration, and removal steps. If intermediate
   states cannot pass independently, keep them on one integration branch and reserve dependent work
   until the integrated behavior passes.
4. Record the graph in the brief with each slice's owner, status, dependencies, and
   revision/evidence pointers. The ready frontier contains unclaimed slices whose prerequisites have
   passed integrated verification. Creating child tickets is not required. Ask for a product
   decision only when decomposition reveals one.

**Done:** every criterion belongs to a slice with an observable result, and the next unblocked slice
has a known baseline.

## Execute and integrate

1. When several slices need the same unresolved exploration, assign one exploration owner to save
   findings with source/revision pointers in a location accessible to the workers. Link the notes
   from the brief; workers check their applicability when the relevant source changes.
2. Give each selected ready slice to one implementation owner using
   [implementation](../anaphor/references/implementation.md). Default to sequential work in the
   supplied checkout. Parallelize independent slices only when their writable code and runtime
   resources are isolated and an owner can integrate them. Record ownership before dispatch. Each
   isolated worker confirms its branch starts from the assigned integration revision; preserve
   existing work and correct a mismatched baseline before implementation.
3. Inspect the returned commits, review dispositions, and criterion evidence. Accept the slice only
   when its required checks pass. Keep incomplete or blocked slices off the ready frontier for
   dependent work.
4. One integration owner lands accepted changes serially. Recheck the integration tip before each
   merge; if it advanced since the worker's baseline, reconcile against the current tip and inspect
   the combined diff. Resolve conflicts from both changes' intended behavior and requirements.
   Verify affected accumulated behavior with [anaphor-verify](../anaphor-verify/SKILL.md). A result
   on an isolated branch does not establish that the integrated state works. Update the graph with
   the integration revisions and evidence before releasing dependents or selecting more work from
   the ready frontier. A failed integration check returns to the implementation owner; dependent
   slices remain blocked until it passes.
5. When all slices are integrated, return the original baselines, final revisions, and complete
   criterion coverage to the coordinator for whole-change review and delivery. Standalone use
   reports this integrated result; it does not silently open PRs.
6. Preserve commits and evidence before cleaning up worktrees created for this run. Remove only
   owned worktrees whose work is integrated or otherwise recoverable; report any retained worktree
   and its remaining work, including when the run stops early.

**Done:** every requirement has reviewed, verified implementation on the integration branch, with
evidence applicable to the accumulated state. A required verification blocker stops dispatch under
`anaphor-verify`.
