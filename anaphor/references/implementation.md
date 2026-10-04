# Implement one slice

1. Read the slice's criteria, confirmed test boundaries, and affected feature recipes. Trace the
   current path through callers, data, and owning modules. Use the project's setup pointer for
   missing prerequisites; keep provisioning outside this procedure.
2. Read Matt's `tdd` under the [composition rules](dependencies.md). For each behavior, observe a
   failing test at the agreed public boundary, implement enough to pass, and repeat. For a bug,
   reproduce the reported symptom and retain a regression that fails for that cause. A failure
   caused only by missing setup is not the regression proof.
3. Update affected feature recipes as the behavior changes. If coverage is missing, use
   [anaphor-create-feature-map](../../anaphor-create-feature-map/SKILL.md) for the affected
   behavior. Preserve accepted outcomes when repairing selectors or harness instructions.
4. Create a scoped commit using repository conventions, retaining the slice baseline. Use
   [anaphor-review](../../anaphor-review/SKILL.md) on the slice. Address findings and perform
   review-driven refactoring under behavior tests. Repeat the checks affected by those changes.
5. Run [anaphor-verify](../../anaphor-verify/SKILL.md) against the resulting revision, including the
   changed feature recipes. If browser behavior is part of a criterion, a unit test alone cannot
   discharge it.
6. Return the commits, criterion results, feature-map changes, review findings and dispositions, and
   evidence locations. Leave owned resources in the state documented by the verification recipe.

**Done:** the slice's criteria pass on its recorded revision, the relevant recipes are executed, and
blocking review findings are resolved. A failed product check returns to step 2; a required
verification blocker follows `anaphor-verify` and stops the run.
