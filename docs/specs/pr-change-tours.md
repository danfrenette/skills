# PR change tours implementation spec

## Outcome and scope

Every PR delivered through Anaphor gets a guided tour that helps its owner decide whether to merge.
The tour explains the problem and value, follows the primary vertical slices through the
implementation, and connects each slice to its specification and verification evidence. It replaces
the generated Markdown delivery walkthrough. Reusable verification recipes remain in their owning
repositories.

Evolve `anaphor-explain-change`; retain its name and existing composition guidance. Use the Anaphor
application for both local and hosted reading. Local preview is the default and requires neither
authentication nor publication. Hosting is an explicitly requested operation using the same content
and media.

This spec covers `/Users/danfrenette/code/anaphor` and `/Users/danfrenette/code/skills`. Product
decisions below were agreed in the planning conversation. Proposed implementation boundaries and
acceptance criteria make those decisions executable. The final acceptance exercise is a tour of
these changes across both repositories, followed by the owner's assessment of its usefulness.

## Current implementation

The inspected Anaphor baseline is `14d85d9`, matching fetched `origin/main` on October 14, 2026.
Uncommitted work in that checkout is outside this spec and must be preserved during implementation.

The application has a shared text reader, a version 1 document schema, owner authentication, device
login, Postgres persistence, and idempotent creation through its CLI. Documents identify
participating PRs with complete base and head SHAs. Section paragraphs render as plain text. The
existing contract does not support local unauthenticated loading, embedded evidence media, or
updates to existing tours.

The skills repository currently requires durable Markdown walkthroughs in
`skills/software-factory/anaphor-explain-change/SKILL.md`. Its composition reference already covers
scenarios, decisions, source anchors, screenshots, recordings, and evidence limits. Verification
receipts are a separate evidence record whose format can follow the project; feature recipes are
reusable instructions rather than per-run reports.

## Reader experience

### T1 Explain the change in vertical slices

Open with the problem, affected user, changed experience, and value. Identify participating PRs and
their pinned revisions. Each primary vertical slice explains its entry point, important ownership
and decisions, implementation path, observable outcome, and consequential failure behavior. Link
source locations at pinned commits and explain why those locations matter.

Keep verification beside the slice it supports. Show the spec criterion, actions or checks
performed, observed result, tested revision, evidence, and limits. Finish with remaining merge
concerns and rollback constraints where relevant. Scale depth to the change; a small documentation
PR still gets a proportionate tour and evidence of the relevant review or checks.

Use continuous reading with section navigation and stable anchors. Readers can jump between slices
without following a mandatory sequence. Preserve usable light and dark themes, keyboard navigation,
narrow reflow, and accessible names. Show broken or unavailable evidence explicitly.

### T2 Display evidence where it proves behavior

Support inline screenshots with alternative text and captions, and videos with native controls,
captions or an equivalent textual account, and no automatic playback. Associate each capture with
its action, observed result, target, and tested revision. Use screenshots for useful visible states
and videos for behavior that depends on interaction or time. Nonvisual changes use appropriate
command output, API observations, or other durable evidence.

Agent-browser is the default capture tool where the project's verification contract permits it.
Preserve the designated harness when a project selects another tool. Captures illustrate observed
behavior; they do not independently establish persistence, authorization, or an unobserved effect.
Diagrams and explanatory examples remain distinguishable from execution evidence.

## Content and evidence contract

### T3 Share a versioned document contract

Extend the environment-neutral schema used by the CLI and reader. Give slices, claims, evidence
records, and assets stable identifiers so updates preserve anchors and relationships. Support:

- Tour identity, title, problem/value overview, ordered sections, and tour revision.
- Participating repository/PR identities and complete current base/head SHAs for each PR.
- Slice explanations, spec references, pinned source links, and consequential decisions.
- Verification records with criterion, expected and observed outcomes, actual action, result
  (`pass`, `fail`, `blocked`, or `not run`), target/build, role/data context, and tested source
  state.
- Asset references, media type, caption, accessible description, content hash, and provenance.
- Evidence applicability (`current`, `stale`, or `unknown`) separate from the recorded test result.

Use explicit validated links and media references rather than arbitrary HTML or executable content.
Documents refer to logical asset IDs; local paths and hosted storage keys are resolved outside the
reader. Keep the reader independent of authentication, filesystem access, and storage providers.

Continue reading existing version 1 text tours. Validate new documents and assets before committing
an update. Define concrete schema limits and supported image/video formats in the implementation,
with actionable diagnostics for unsupported or oversized input. Do not copy media bytes into JSON.

### T4 Preserve evidence provenance as the PR changes

Update one logical tour for a PR rather than creating an unrelated tour for each edit. Increment its
revision and preserve previous evidence records with their original tested source state. The tour
revision and tested source revision are distinct concepts.

On a PR head change, evidence against an older source state becomes stale by default. It may remain
applicable only when an agent inspects the delta and records why the tested behavior is unchanged;
retain the original test revision, date, and applicability rationale. A rerun creates a new evidence
record and may supersede an earlier one. Never relabel an old run as having tested the new head.

For uncommitted work, retain a patch and relevant untracked contents or hashes with the receipt;
HEAD alone is insufficient. Associate each participating repository with its own source state.
Applicability follows the actual source and build used, including changes after a capture.

The reader prominently identifies stale and unknown required checks. A historical pass remains a
historical pass. Missing, failed, blocked, unrun, stale, or unknown required evidence prevents a
merge-ready claim. A tour presents evidence and concerns; the owner makes the merge decision.

## Local application support

### T5 Persist tours outside product repositories

Introduce a configurable persistent local Anaphor workspace with a documented default in the user's
application data directory. Group content by repository and PR while retaining a stable tour ID.
Copy accepted captures and receipts into that workspace before implementation scratch is cleaned up.
Keep documents, referenced assets, retained source-state evidence, and update metadata together.

Provide CLI operations to validate a prepared tour bundle, create or update the local tour, and
return its preview URL. Exact command syntax belongs in CLI help and the development guide. Once a
PR exists, persist its association so later invocations find the same tour. A coordinated change may
share one tour across participating PRs; each PR links to its relevant section.

Apply document and asset changes atomically: readers see a complete prior or complete next revision.
An interrupted or invalid update preserves the last readable revision. Detect conflicting writes
against a supplied expected revision and report recovery guidance. Refresh explicitly to load a new
revision, preserving existing reader behavior.

### T6 Preview without hosted prerequisites

Load the workspace through a local-only entry point in the existing Next.js application and render
through the shared tour reader. Local reading needs no OAuth credentials, device login, database,
secure-store entry, hosted media provider, or publication. The public manual remains available.

Enable local access explicitly in a loopback-bound application instance. Production and preview
deployments must not expose an unauthenticated filesystem-backed tour path. Resolve document and
asset IDs within the configured workspace; reject traversal and symlink escape. Serve only
registered assets rather than accepting arbitrary filesystem paths from a request. Support video
seeking.

Return a clear missing-tour or missing-asset state. A running reader continues to use its selected
revision until explicit refresh; session handling for hosted tours retains its existing boundaries.
Local preview URLs are for the current machine and are labelled accordingly in PR handoff text.

## Hosted continuation

### T7 Publish the same tour on request

Extend authenticated publication to accept the shared document and referenced assets, including
updates to an existing hosted tour. Preserve stable hosted identity, source/evidence provenance,
expected-revision conflict handling, and unchanged-retry idempotency. Retrying an uncertain response
must not create another tour or substitute different content under the same operation key.

Hosted tours and their media remain owner-only. Store media privately and enforce access through the
hosted read path, including video requests. Publish a complete readable revision only when its
document and required assets are available. Interrupted publication leaves the local tour usable and
the prior hosted revision intact; retain the operation key and bundle for recovery.

Hosting changes delivery location, not the authored narrative or rendering. It remains optional for
local delivery. Real-provider and deployed publication acceptance are separate from local browser
success, following the existing private-tour environment gates.

## Skill and delivery integration

### T8 Evolve anaphor-explain-change

Keep the skill name. Replace its Markdown-output requirement with this authoring process:

1. Read the accepted spec, participating PRs and pinned changes, decision records, and receipts.
2. Plan the problem/value opening and primary vertical slices using the existing composition guide.
3. Obtain required missing verification through `anaphor-verify`; preserve actual capture
   provenance.
4. Create or update a validated tour bundle in the persistent workspace and preserve evidence files.
5. Open the local Anaphor preview. Inspect navigation, text, source links, media, evidence
   references, and freshness against the delivered source states. Repair and recheck failures.
6. Return the preview URL and relevant tour/source revisions. Publish and verify a hosted URL only
   when requested; use the same bundle and retain recovery metadata.

Put operational command and environment details in a focused integration reference reached from the
skill. Keep composition guidance authoritative for the narrative and verification guidance
authoritative for execution evidence. The app's schema and CLI help own exact fields and commands.
Update the skill's invocation description so standalone requests to explain a PR as a tour reach it.

### T9 Make tours the delivery default

Update `anaphor` delivery, `anaphor-reconcile`, relevant README guidance, and attribution wording to
replace the required published Markdown walkthrough with a verified local tour or requested hosted
tour. Every PR delivered through this workflow gets a link. For a shared tour, record all
participating PRs and their dependency order and validate the sections relevant to each one.

Keep existing recipes and historical walkthroughs readable. New delivery does not create a second
Markdown narrative or require explanation-only commits. Durable product documentation and recipe
updates still follow their repository rules. Receipts can remain distinct artifacts linked from the
tour, with durable copies or resolvable references that survive worktree cleanup.

An inspected local preview satisfies tour delivery for solo review; external readers need a hosted
URL and appropriate access. A broken preview, unresolved required evidence, or invalid provenance
leaves delivery incomplete. Creating a draft PR, completing a tour, declaring merge readiness,
merging, and deploying remain distinct actions.

## Implementation slices

1. **Local text tour:** introduce the compatible document contract, persistent workspace, atomic
   updates, CLI workflow, and unauthenticated local entry point using the shared reader (T1, T3–T6).
2. **Evidence reading:** add evidence associations, applicability, managed captures, inline media,
   and reader status presentation (T2–T6).
3. **Skill integration:** evolve authoring and delivery guidance and exercise it against a real
   local tour (T8–T9). Local acceptance can complete independently of hosted provisioning.
4. **Hosted continuation:** add private assets and authenticated updates without changing the local
   authoring workflow; verify the configured isolated environment (T7).
5. **First-use evaluation:** explain these application and skill changes through the resulting tour,
   verify it in the browser, then collect the owner's assessment (T10 below).

Keep the application behavior in `apps/demo/features/tours` and related routes. The design-system
package supplies presentation through public exports. Select concrete persistence layout, routes,
commands, and schema representation during implementation, retaining these observable contracts.

## Verification and acceptance

Add or update reusable recipes in the Anaphor app repository. Follow its testing and review gates;
exercise meaningful public CLI, request, and reader behavior rather than private implementation
structure. Required coverage includes:

- **T1–T3:** a representative multi-slice tour renders specs, pinned code links, checks, images, and
  playable video. Test keyboard operation, light/dark themes, narrow reflow, and accessible media.
  An existing version 1 tour remains readable. Invalid content produces actionable diagnostics.
- **T4:** changing one participating PR head preserves original results and revisions while exposing
  stale evidence. A documented unaffected-delta assessment and a fresh rerun remain distinguishable.
  Missing or stale required checks prevent a merge-ready claim.
- **T5:** create, restart, reopen, update, and explicitly refresh the same tour. Remove the owned
  scratch worktree and confirm imported evidence remains usable. Invalid, interrupted, and
  conflicting updates preserve the prior revision and return accurate errors.
- **T6:** preview with all hosted credentials/services absent. Check missing assets, seeking, path
  containment, disabled local routes in deployed mode, and independent public-manual access.
- **T7:** authenticated publish/read/update with private media; denied unauthorized document and
  asset requests; safe retry and conflict behavior; failed uploads preserve the prior revision.
  Record isolated-environment acceptance separately from real-provider/deployed acceptance.
- **T8–T9:** run the revised skill on an implementation PR and on a small nonvisual PR. Observe that
  each gets a proportionate tour, uses appropriate evidence, opens the actual reader, and returns a
  usable URL. Inspect affected guidance for contradictory Markdown/publication requirements.

### T10 Evaluate the workflow using its own changes

Create one coordinated tour for the application and skills PRs produced by this implementation.
Explain local loading and persistence, evidence/media and freshness, and authoring/delivery as the
primary slices. Include this spec, both repositories' pinned source states, and their dependency
order. The tour must use the implemented local workflow, without a Markdown walkthrough substitute.

Capture screenshots of the actual reader and video where it demonstrates useful behavior such as
refreshing a tour after a PR change. Capture evidence before cleanup and import it into the managed
workspace. Inspect the final tour after its last update; distinguish tests of application behavior
from inspection of the explanatory artifact. Retain the final inspection receipt outside the tour
when embedding it would create an endless cycle of tour updates.

Give the owner the working local URL and ask whether they can identify the problem/value, follow
each primary implementation slice, inspect the evidence, spot stale or missing checks, and decide
what remains before merge. Record their feedback separately from automated acceptance. Repair
identified explanation or reading problems and repeat the affected inspection. Technical completion
requires passing checks and a working tour; usefulness remains unconfirmed until the owner reviews
it. A spec or an uninspected generated bundle does not satisfy this evaluation.

## Boundaries and migration

No historical Markdown conversion, public sharing model, browser-based authoring studio, mandatory
stepper, embedded diff editor, or automatic merge/deploy action is required. Existing private access
rules continue to apply to hosted content. Local preview does not establish hosted launch readiness.

Roll out the skill's required tour handoff after local loading, evidence rendering, and inspection
are available. Preserve existing hosted version 1 documents during schema evolution. Keep local
bundles and previous readable revisions recoverable when an update or publication fails. Any hosted
database migration follows the repository's backup and isolated-environment acceptance procedure.
