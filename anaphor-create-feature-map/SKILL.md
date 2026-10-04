---
name: anaphor-create-feature-map
description:
  Create or extend project-local verification recipes when changed behavior lacks a feature map or
  repeatable coverage.
---

# Anaphor: create a feature map

Write a recipe a fresh agent can execute without the originating conversation. Read the
[recipe format](references/recipe.md). Keep setup facts in project-owned instructions and map
entries in the owning repository.

1. Inspect the affected routes, commands, interfaces, tests, and documented launch procedure.
   Identify the changed outcome, its entry points and roles, data prerequisites, and observable
   effects. Scope automatic creation to the affected feature; whole-app discovery is separate work.
2. Find the existing project verification skill or map through repository instructions. Extend that
   location. If absent, use the repository's configured local-skill directory for
   `verify-<app>/SKILL.md`, `features/README.md`, and feature files. When no local-skill discovery
   convention exists, use `docs/verification/` with an index and recipes, then add a short pointer
   in the repository's existing contributor or agent guide. If no guide exists, point from the
   repository README. Report the chosen location.
3. Write launch, doctor, drive, evidence, and cleanup instructions from inspected commands and real
   handles. Link authoritative setup instructions instead of reproducing provisioning steps. For a
   generated local skill, include a name and description identifying its app, surface, and trigger.
4. Write one recipe per affected feature using the shared format. Index the entries and coverage
   limits. A library feature can be an executable public-interface test; browser instructions are
   required only for browser behavior.
5. Run every new or changed recipe through launch, doctor, drive, capture, and cleanup. Apply
   [evidence and blockers](../anaphor-verify/references/evidence.md) directly; do not recursively
   invoke map creation. Confirm artifacts survive cleanup and repair instructions that fail.

**Done:** each generated recipe was executed successfully against the intended behavior and can be
found from the project's instructions. If any required recipe is blocked or fails, preserve it as a
draft and report that result; successful neighbors do not certify it.
