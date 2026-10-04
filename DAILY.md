# Daily maintenance

Maintain Anaphor's external disciplines and source guidance. Run from this repository when asked for
daily maintenance. This file defines the work; scheduling it is a separate setup step.

## Establish the baseline

Read `git status`, [skills-lock.json](skills-lock.json), the
[dependency contract](anaphor/references/dependencies.md), and the
[last source review](docs/maintenance/upstream-review.md). Preserve existing work. If a maintenance
edit overlaps an unrelated local change, prepare it separately and report the overlap.

The lock is the inventory of installed dependencies. The dependency contract owns when they run; the
[Principles profiles](anaphor-review/references/principles/README.md) own language-specific checks.
[Attribution](anaphor/ATTRIBUTION.md) records provenance, not a moving latest-version list.

Use `skills@1.7.0` for the commands below. Review CLI upgrades separately because discovery, lock
semantics, and update commands can change. Scope every install or update to a temporary project or
this project; global installations belong to the user.

## Inspect upstream changes

1. Create a temporary directory outside this repository. Copy `skills-lock.json` and the current
   `.agents/skills/` directory into it, keeping a separate baseline copy for comparison. If
   installed copies are missing, use the restore procedure in
   [README.md](README.md#maintaining-this-repository) in the temporary directory. A restore that
   changes hashes is a candidate update, not a recovered baseline; obtain the old content from a
   known source snapshot or report the comparison blocked.
2. From that temporary project, run `npx --yes skills@1.7.0 update --project --yes`. Inspect each
   dependency's result and compare the generated lock and changed file contents with the baseline. A
   successful process exit alone does not establish that every dependency was checked. Record failed
   fetches, missing skills, and unresolved sources individually.
3. Review every changed dependency for altered triggers, required tools, model assumptions,
   confirmation steps, side effects, references, and license terms. Read its changed supporting
   files as well as `SKILL.md`. Follow renamed or removed references before calling it compatible.
4. For pstack and Matt's `to-spec`, compare upstream with the revision in the source-review record.
   Inspect changes affecting orchestration, accepted-spec shape, review depth, verification, feature
   maps, and explanations. These are guidance sources, not installed dependencies.
5. Check the primary-source links in the Principles profiles and any live guidance fetched by a
   dependency. Compare relevant changed guidance with the local checks. The lock covers downloaded
   files; it does not freeze the contents of URLs those files fetch. Report inaccessible required
   comparisons rather than treating them as unchanged.

This stage is complete when each dependency and guidance source is classified as unchanged, changed
and inspected, or blocked with a concrete reason.

## Adopt compatible changes

Assess changes against the dependency contract and
[deliberate Anaphor choices](anaphor/ATTRIBUTION.md#deliberate-anaphor-choices). Keep accepted-spec
entry, project-owned setup, inherited-model role separation, confirmed testing decisions, required
verification gates, and draft-PR delivery intact.

For compatible updates, copy the CLI-generated entries and matching downloaded directories into this
project together. Preserve upstream files byte-for-byte. Put Anaphor-specific adaptations in its
dependency contract or applicable review profile. Use the CLI to add or remove dependencies; never
invent hashes or maintain a second dependency inventory.

If an update conflicts with these policies, retain the current entry and installed copy. Describe
the conflict and a proposed adaptation for review. Partial adoption is allowed: retain the exact
previous entries for deferred skills and use the exact generated entries for accepted skills. List
every deferred or blocked item so a partial update cannot look complete.

Update the source-review record only through revisions actually inspected. Record adopted or
deliberately deferred guidance and unresolved decisions. Preserve the original attribution pins;
append new provenance when new guidance is incorporated. Avoid date-only edits when nothing changed.

## Verify and report

- Run `npx --yes skills@1.7.0 list --json` and confirm all locked skills are installed locally.
- Run `npx --yes skills@1.7.0 add . --list` and confirm installed dependencies are excluded from
  this repository's published catalog. Compare against the authored root-level `SKILL.md` files.
- Run Prettier's Markdown check with this repository's configuration and ignore file. Verify local
  links, skill names, and frontmatter in changed authored files. Formatting excludes downloaded
  dependencies because changing their bytes would invalidate their recorded content.
- Trace each changed instruction through its triggering branch and completion condition. For changes
  affecting runtime behavior, run a focused scenario and record its inputs, observed behavior, and
  limits in [validation notes](anaphor/VALIDATION.md). If the environment prevents a trial, label
  the change unvalidated and name the missing prerequisite.
- Inspect the final diff for unrelated edits, lock/copy mismatches, and unintended policy changes.

Finish with the adopted updates, deferred decisions, verification results, and concrete blockers.
Prepare a reviewable local diff; commit or publish a draft PR only when that run authorizes it.
Unchanged runs need no repository edits. A blocked comparison or unrun required trial remains
explicitly incomplete.
