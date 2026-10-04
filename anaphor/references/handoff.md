# Draft PR handoff

1. Confirm complete-change review, required tests, behavior verification, and affected feature-map
   updates cover the result being delivered. Commit intended changes using repository conventions.
   For multiple repositories, record their revisions and integration/deployment dependencies
   together.
2. Push the verified branches and open **draft** PRs using the host's supported workflow. Include
   the spec, user-visible outcome, consequential domain decisions, scope, verification evidence and
   limitations. Link related PRs and explain their dependency order. Required blocked or unrun
   checks prevent this step.
3. Use [anaphor-explain-change](../../anaphor-explain-change/SKILL.md) to write the durable
   walkthrough. Publish it to the repository's established review-document location; when none
   exists, use `docs/change-walkthroughs/<change-slug>.md` in the primary repository. Link it from
   every participating PR.
4. Review the explanation commit and validate its links against the implementation revisions. If its
   diff changes only explanation documents, preserve the earlier test provenance and record why
   application checks are unaffected; do not claim those tests ran again. Any executable,
   configuration, or feature-recipe change returns to affected review and verification. Check final
   PR heads and draft status after the last push.
5. Report the draft PRs, published walkthrough, implementation and final head revisions, and
   criterion evidence. If publishing fails, report the partial handoff and resume it without
   duplicating PRs.

**Done:** each PR remains draft, links a readable walkthrough, and has review and verification
evidence applicable to its final contents. Marking ready, merging, and deployment are separate user
decisions.
