---
name: anaphor-audit-feature-map
description:
  Audit an existing feature map against source and live behavior when its coverage or recipes need a
  complete check.
---

# Anaphor: audit a feature map

Audit the entire named map. Ordinary implementation uses `anaphor-verify` for affected entries; this
operation accounts for every mapped feature. Limit edits to verification documents and their owned
harness helpers.

1. Read the index and every recipe, then compare them with routes, commands, tests, and recent
   behavior changes. Record missing, duplicate, and stale coverage. If there is no map, report that
   fact and route creation through
   [anaphor-create-feature-map](../anaphor-create-feature-map/SKILL.md).
2. Identify intended outcomes from accepted requirements and project documentation. Prepare the
   target through its documented launch/doctor instructions. One owner drives shared app state;
   source-reading work may use separate read-only contexts under
   [agent handoffs](../anaphor/references/agents.md).
3. Execute every mapped recipe, covering the entry points and roles that change outcomes. Record
   evidence using [evidence and blockers](../anaphor-verify/references/evidence.md). After a
   surprising failure, run doctor and classify the discrepancy before continuing. An unresolved
   prerequisite stops execution; mark remaining entries not run.
4. Repair descriptions or recipes that have drifted from working intended behavior, then re-drive
   changed recipes. Report product regressions to implementation, retaining the intended assertion.
   Reset owned state before the next independent recipe when a failure contaminates it.
5. Validate the index and links, clean up owned resources, and confirm proof artifacts survive.
   Report document outcome separately from product outcome: documents unchanged or corrected; each
   feature pass, fail, blocked, or not run.

**Done:** every map entry has source coverage and a live result or an explicit coverage gap. A
complete report may identify product failures; only all required passing results establish verified
behavior. Corrected recipes remain unverified until their live execution passes.
