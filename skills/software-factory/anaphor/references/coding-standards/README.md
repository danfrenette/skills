# Resolve coding standards

Run this procedure before implementation, design comparisons, or Standards review. Resolve each
owning repository separately; a missing standards file is not permission to borrow another
repository's architecture.

1. Read repository instructions and locate `CODING_STANDARDS.md`, including scoped files governing
   the affected paths. Follow its applicable references. If the repository supplies standards there
   or points to an equivalent authoritative document, use those standards and stop fallback
   selection. A short router counts as an existing standards file.
2. Only when repository standards are absent, inspect dependency manifests and affected source:
   - Rails application or API: use [Rails API](rails/CODING_STANDARDS.md) for its application/API
     code. Server-rendered UI still needs the project's presentation conventions.
   - Ruby library or gem without Rails: use [Ruby library](ruby/CODING_STANDARDS.md).
   - Next.js: use [Next.js](nextjs/CODING_STANDARDS.md) plus [React](react/CODING_STANDARDS.md); add
     [TypeScript](typescript/CODING_STANDARDS.md) for typed code.
   - React without Next.js: use React; add TypeScript for typed code.
   - TypeScript without React: use TypeScript alone.
   - Mixed stack: apply each matching layer to its own paths. A Rails/Next.js repository uses both
     backend and frontend entries. Plain JavaScript can use React/Next.js rules without adopting
     TypeScript; other uncovered languages retain an explicit coverage limit.
   - No matching sample: record that standards are unavailable for that surface. Continue discovery
     from repository instructions and accepted requirements; identify unresolved conventions before
     dependent implementation. General Principles guidance stays labelled as judgment.
3. Read the selected sample's core rules, then every reference triggered by the planned change.
   Record the repository, governed paths, selected source/version, loaded references, and any
   uncovered surfaces in the implementation or review brief. Pass that selection to workers and
   reviewers; standalone review resolves it using the same procedure.
4. Apply defaults within the accepted scope and existing public contracts. Preserve a documented
   compatibility requirement or accepted architectural decision over a conflicting sample rule;
   record the specific exception and evidence. A fallback does not authorize replacing a result
   library, serializer, public API, error policy, or deployment topology. An unexplained legacy
   style alone is not an exception. If compliance requires a migration beyond the task, flag the
   conflict and resolve that design choice before changing the affected boundary.

**Done:** each affected surface has repository standards, an identified fallback with its applicable
references, or an explicit coverage limit. Standards findings cite that resolved authority; an
unassessed surface remains visible in the review's evidence limits.

## Samples and adoption

The samples are active fallback standards when selected above. Read them in place from the installed
Anaphor skill; selection does not create or overwrite files in the destination repository. To adopt
a sample permanently when requested, copy this directory as a bundle, point the repository's root
`CODING_STANDARDS.md` at the chosen entry, and adapt the contracts to that repository. Preserve the
relative links to shared Ruby references. An adopted repository copy becomes its own authority.

Keep samples inside `anaphor` so a normal skill installation includes their references. New profiles
need a stack trigger here, a concise `CODING_STANDARDS.md`, and branch-specific references. Put
rules needed by every branch in the entry file; disclose rules needed by only some changes. Give
each meaning one owner rather than repeating it across profiles.

## Provenance

Rails starts from Autodidact's planning-folder `CODING_STANDARDS.md`, read October 28, 2026. That
copy contains the October 11 decisions assigning endpoint status policy to feature results and
requiring use-case preconditions; the implementation checkout's copy predates those revisions.
Retained: REST resources, fixed use cases, Jbuilder, explicit inputs, named results, failure
sequencing, transaction ownership, and outcome tests.

Ruby additions come from Substrate's `CODING_STANDARDS.md` at
`f61e39c899c167498173800a35286853c7539923`. Retained: bareword business orchestration for Ruby
library commands, argument/default decisions, construction idioms, resource ownership, verification
command placement, and public-interface tests. Its `Substrate::Command` failure wrapper remains
specific to that gem; Rails' reporting/re-raise policy remains separate.

Project names, framework version snapshots, deployment vendors, telemetry provisioning, legacy-copy
authorization, audio installation options, and historical delivery evidence are excluded from the
Ruby/Rails samples. Frontend conventions have their own entries. The disclosed Rails result
compatibility reference describes the source's custom base; it does not claim Rails provides that
API or require copying it into an existing application.

These are local conventions informed by the source documents, not universal Rails/Ruby rules. The
service-size and parameter thresholds remain review heuristics, distinct from mandatory
responsibility and failure rules.

React/Next.js performance guidance references Vercel's public `react-best-practices` and
`composition-patterns` skills; detailed examples remain upstream and load by concern. Folder
colocation and route/screen/section ownership are local conventions requested October 28, 2026,
building on Autodidact's frontend composition section and Kent C. Dodds's colocation principle.
TypeScript references Matt Pocock's Total TypeScript and scoped adaptations from Rhys Sullivan's
`quality-code`; each entry links its sources and applicability limits. External sources were
inspected October 28, 2026. Framework-specific examples must match the destination's pinned
versions.

The supplied _Sustainable Rails_ excerpt, chapter 15 (pages 219–230) and section 16.1 (page 231),
informs the Rails application boundary, collaborator selection, caller-oriented outcomes, and the
distinction between validation feedback and database integrity. The adaptation retains `.call` with
fresh instances and existing shared result infrastructure; the
[boundary reference](rails/service-boundary.md) records those departures. The excerpt is reference
material, not a repository artifact or an instruction to change accepted invocation contracts.
