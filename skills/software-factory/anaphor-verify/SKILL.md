---
name: anaphor-verify
description:
  Verify changed behavior with repository tests and real user flows, update affected feature
  recipes, and report revision-bound evidence or blockers.
---

# Anaphor: verify behavior

Prove the accepted outcomes on the surface where they occur. Read
[evidence and blockers](references/evidence.md) before running checks. Project setup owns
provisioning; this skill owns execution and observed results.

## Select and prepare

1. Read the criteria, changed paths, project verification instructions, and relevant feature map.
   Select all affected entry points and roles that change the outcome. Update altered recipes and
   remove obsolete ones. For missing coverage, use
   [anaphor-create-feature-map](../anaphor-create-feature-map/SKILL.md); read its shared
   [recipe format](../anaphor-create-feature-map/references/recipe.md) when editing an existing map.
2. Identify the delivered source revision and the running target's corresponding build. Record local
   changes when testing an uncommitted state. Check the target, health, identity/role, and required
   data using the documented read-only doctor procedure. Start only the services needed by these
   criteria.
3. Choose the existing repository harness first. For browser-visible behavior, run its real browser
   flow with agent-browser or Playwright; read the installed tool's instructions for current
   commands. For a CLI, service, or library, exercise its public command, request, or interface.
   Record a required unavailable tool as a prerequisite failure, not a reason to substitute a weaker
   surface.

## Execute and observe

1. Run focused behavior tests and required repository checks. Preserve failing-then-passing evidence
   for regressions; a green suite does not prove an unexercised criterion.
2. Execute every selected feature recipe, including alternate routes or roles relevant to the
   change. Reuse a recipe's creation-time proof only when it covers the same criteria on the
   unchanged target and source state. Capture the action and resulting state. For browser flows,
   confirm usable controls and the claimed outcome; a successful HTTP status or redirect alone is
   insufficient.
3. Check relevant persisted effects through the public read path, reload, or subsequent user action.
   Additional isolated data inspection can corroborate runtime evidence; it does not replace a
   public-interface TDD assertion. Exercise each criterion's required failure case and a meaningful
   affected failure path where one exists.
4. After a surprising result, run doctor again. Distinguish broken product behavior from a stale
   recipe or unavailable prerequisite under the blocker procedure. Fix recipe drift only against the
   accepted behavior, then execute the corrected recipe.
5. Capture the result before cleanup. Stop only owned processes/sessions and remove only owned
   scratch state when safe. Confirm evidence survives teardown. If the documented run deliberately
   retains a service, report its owner and location.

**Done:** every selected criterion has a passing observed result on the matching surface, affected
recipes are current and executed, required checks pass, and evidence identifies the tested contents.
Failed product checks return to implementation; unresolved required prerequisites stop the run.
Full-map auditing is a separate [audit](../anaphor-audit-feature-map/SKILL.md).
