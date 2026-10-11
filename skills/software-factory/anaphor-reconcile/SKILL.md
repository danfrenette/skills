---
name: anaphor-reconcile
description:
  Update affected project records after accepted planning decisions or verified implementation.
  Use when product, domain, setup, or tracker documentation must reflect a changed decision or
  proven behavior.
---

# Anaphor: reconcile project records

Read Matt Pocock's installed writing-for-agents skill before editing. It governs these records,
including human-facing product documents. Resolve external skills through the host's installed
catalog and project dependency lock; if a required skill is absent, report it and stop that branch.

## 1. Classify the evidence

Read the accepted decision or spec, changed paths, project instructions, and verification receipts.
For each changed claim, choose the supported state:

- Accepted decision only: record planned behavior and unresolved questions.
- Code inspected without a passing receipt: record implementation as unverified.
- Passing receipt: identify the tested revision, surface, and environment.
- Deployment evidence: identify the deployed revision and environment separately.

If behavior contradicts accepted intent, preserve the requirement and report the implementation
gap. Rewriting the requirement would hide a regression. Continue independent supported updates.

## 2. Find the owner

Follow project pointers to the affected product record, glossary/ADRs, development guide, feature
map, and tracker. In the existing brief or temporary notes, pair each changed claim with its owning
record and evidence. Use the existing canonical home; creating another summary makes future drift
more likely. If ownership is ambiguous, resolve it before editing that claim.

Limit this pass to the change. Empty documents and unrelated historical cleanup do not help
prove it.

## 3. Update by record type

- Product record: replace stale current-state prose in place. Keep accepted future scope distinct
  from verified behavior, and link useful history rather than appending contradictory instructions.
- Glossary or ADR: when a resolved term or consequential decision changes, read Matt Pocock's
  installed domain-modeling skill and follow the project's locations and conventions. Preserve
  prior rationale when linking a successor; leave missing decisions open rather than inventing them.
- Development or navigation: check affected commands, paths, and prerequisites against the owning
  repository. Label an unexecuted procedure as unverified; inspection is not proof that it runs.
- Feature map: link the receipts maintained by anaphor-verify. Return stale recipes or missing
  execution evidence to verification, which owns their live proof.
- Tracker: update evidence links and blockers only within the authorized scope. Preserve unrelated
  relationships and parent-issue restrictions. An open draft PR does not mean deployed behavior.

Each affected record must be updated, unchanged with a reason, or blocked by a named prerequisite.
Link existing specs and walkthroughs instead of copying their narrative into these records.

## 4. Check the result

Review the documentation diff and links against the evidence. Apply writing-for-agents to remove
duplication and repair navigation. Use the project glossary and enough context for a person who has
not read the conversation. If no record needs a change, report that result without creating files.

Documentation-only changes can retain prior code-test evidence with its revision and limits.
Executable, configuration, or recipe changes return to affected review and verification. After
publication, update affected delivery links from actual PRs and walkthroughs.

Report changed records and concrete blockers through the existing brief or final response.
Standalone use publishes or closes tracker items only when authorized. During Anaphor delivery,
unresolved required records keep delivery open; unrelated documentation debt stays separate.

**Done:** every affected record has a supported disposition, links resolve, and current instructions
distinguish accepted intent from observed behavior without requiring the originating conversation.
