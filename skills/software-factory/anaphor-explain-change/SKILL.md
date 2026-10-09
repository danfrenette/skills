---
name: anaphor-explain-change
description:
  Assemble a durable, evidence-linked explanation of an implemented change, using detailed
  scenarios, diagrams, and measured graphs where they help readers understand behavior and
  verification.
---

# Anaphor: explain a change

Explain an existing implementation for a reviewer. Read the accepted spec, participating PRs or
diffs, relevant surrounding code, and verification receipts. This operation explains evidence; it
does not certify unrun checks.

1. Pin the implementation revisions and identify the participating repositories. Confirm ambiguous
   PR membership before including it. Distinguish accepted intent, observed implementation, supplied
   results, and unresolved assumptions.
2. Read [content composition](references/content-composition.md) to plan the reader's questions,
   explanation depth, visuals, and evidence. Use a short overview to orient the reader, then develop
   each important scenario to the depth needed to understand and assess it.
3. Write durable Markdown in the requested location. During Anaphor handoff, use the repository's
   review-document location or `docs/change-walkthroughs/<change-slug>.md` in the primary
   repository. Standalone use returns the document without posting it elsewhere unless requested.
4. Start with the actor, changed experience, and why it matters. Explain domain terms before using
   them to describe decisions. Include only concepts needed to understand this change.
5. Follow concrete scenarios from entry point through the important responsibilities to the
   observable outcome. Link code at the pinned revisions and explain why each selected location
   matters. Cover cross-repository dependencies and relevant failure behavior. Add a diagram,
   screenshot, or recording when it clarifies a relationship or observed result.
6. Explain consequential choices, rejected alternatives, compatibility or rollout concerns, and the
   questions a reviewer should examine. Use the actual decision record; mark missing rationale
   rather than inventing it.
7. Link verification receipts to their scenarios. Name the tested revisions and limitations,
   distinguishing tests run by this agent from supplied results. Describe blocked or unrun checks
   honestly when explaining an incomplete change outside factory delivery.
8. Check every code anchor and artifact link for reader access. Inspect the document diff and ensure
   no credentials or local-only artifact paths are presented as published evidence. In the
   authorized factory handoff, commit/publish the document and return its durable link for the
   coordinator to add to the draft PRs with a concise behavior summary, key evidence, and concrete
   rollback constraints and affected scope. The PR body is the entry point to the full explanation.

**Done:** a reader can follow behavior, decisions, implementation, and evidence from the document's
links. A local file alone does not complete a requested published PR walkthrough. Hosted or
interactive Tours are optional, separately requested formats.
