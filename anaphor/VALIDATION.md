# Draft validation

Reviewed 2026-10-04. This records structural checks and author walkthroughs, not observed
performance of an agent executing the workflow.

## Structural checks

- Eight skill entry points have matching directory/frontmatter names and descriptions.
- The coordinator is explicitly user-invoked; the seven supporting skills remain discoverable.
- Relative Markdown links resolve with the full family installed as sibling directories.
- The two upstream license notices match the researched source copies.
- Required external disciplines are identified separately from bundled skills and optional
  references.
- Runtime instructions contain no Marketfuel workspace commands, credentials, database names, Linear
  status IDs, model roster, or Cursor-specific orchestration API.

## Dependency maintenance setup

On 2026-10-04, skills CLI 1.7.0 installed eight external disciplines into a temporary project and
generated the root lock. The project copies and lock match that output byte-for-byte. `list --json`
reports all eight as project-local; `add . --list` discovers only the 15 authored skills. Git and
Prettier exclude downloaded dependencies. Authored Markdown formatting and maintenance file links
pass their checks.

The six Matt dependency hashes also match the CLI's folder-hash calculation. The Vercel snapshot
entries use provider-returned hashes, which differ from a local folder hash; those entries retain
the CLI's values. Verification of those copies establishes equality with the downloaded snapshot,
not an independent match to its provider digest.

The daily procedure has not yet been tested through an autonomous update/adaptation cycle.

## Scenario walkthroughs

These are manual traces through the written procedures. They check that the relevant branch and
outcome are present; they do not demonstrate that an executing agent will follow them reliably.

- **Scenario:** Accepted library spec; no browser or tracker

  **Expected route:** Carry confirmed test boundary into TDD; test public interface; create affected
  recipe; review; draft PR

  **Written coverage:** Coordinator, dependencies, implementation, map creation, handoff

- **Scenario:** Browser feature persists a change

  **Expected route:** Exercise user action and public readback/reload; cover relevant failure path;
  update and run recipe

  **Written coverage:** Verify: execute and observe

- **Scenario:** Spec already confirms test boundaries

  **Expected route:** Reuse confirmation; ask only for missing or materially changed boundaries

  **Written coverage:** Dependencies: TDD composition

- **Scenario:** Implementation exposes a product ambiguity

  **Expected route:** Pause affected work; continue independent slices

  **Written coverage:** Coordinator: implementation brief

- **Scenario:** Browser selector drift

  **Expected route:** Repair against working intended behavior; retry once without weakening
  assertion

  **Written coverage:** Evidence: triage

- **Scenario:** Missing login access after safe recovery

  **Expected route:** Stop; report prerequisite and unverified criteria; no draft PR

  **Written coverage:** Evidence: triage; handoff gate

- **Scenario:** Browser reaches the app and finds broken behavior

  **Expected route:** Record failure and return to implementation, preserving expectation

  **Written coverage:** Evidence: triage; implementation

- **Scenario:** Missing map in a repo without local skill discovery

  **Expected route:** Add minimal affected-feature docs and a project pointer; execute every new
  recipe

  **Written coverage:** Map creation

- **Scenario:** Audit finds a product regression

  **Expected route:** Preserve expected behavior; report product failure separately from document
  changes

  **Written coverage:** Feature-map audit

- **Scenario:** Only one model and one worker slot

  **Expected route:** Sequential fresh-context roles with inherited model

  **Written coverage:** Agent handoffs

- **Scenario:** Only one conversation context

  **Expected route:** Named passes with disclosed reduced separation

  **Written coverage:** Agent handoffs

- **Scenario:** Integration changes a previously passing result

  **Expected route:** Rerun affected accumulated checks before accepting dependents

  **Written coverage:** Slices; coordinator; evidence

- **Scenario:** Triggered reviewer cannot inspect required source

  **Expected route:** Mark unassessed; prevent factory delivery

  **Written coverage:** Review completion; coordinator gate

- **Scenario:** Walkthrough adds a documentation-only commit

  **Expected route:** Review document/links; retain test provenance and explain unchanged
  applicability

  **Written coverage:** Handoff

- **Scenario:** Missing Matt TDD or code-review

  **Expected route:** Name dependency and leave dependent step incomplete; no silent replacement

  **Written coverage:** Dependencies

The walkthrough identified and tightened three draft rules: executed recipes must pass, unassessed
required review passes prevent delivery, and unchanged creation-time recipe evidence can be reused
without rerunning it immediately.

## Live validation still required

The Principles-axis extension was also checked by tracing these cases through the written routing:

- Ruby-only change: load Ruby/Rails checks; skip frontend and TypeScript guidance.
- React/TypeScript change: load the JavaScript/TypeScript and frontend profiles; expand only
  relevant Vercel rules and preserve each source's applicability.
- Node-only TypeScript change: apply behavior-test and type-design checks without React assumptions.
- Rails views plus TypeScript components: the Principles agent covers both language profiles and the
  frontend interface checks.
- Documentation-only change: record Principles as not applicable; do not invent a language finding.
- Unsupported language: use grounded project/primary guidance or report unassessed coverage.
- Missing optional Vercel skill: use the linked primary source or local checks with explicit limits;
  do not claim to have applied unavailable rules.
- A profile recommendation conflicts with a documented project decision: respect the decision and
  explain the tradeoff; a formal rule breach belongs to Standards.
- A profile finds a reachable product defect: retain its evidence and cross-reference the owning
  Spec or Execution result without counting it twice.

These are author walkthroughs, not live subagent review results.

UI progressive-disclosure routes were also traced on 2026-10-04:

- Ruby service or Node utility: owning language only; no UI craft or Refactoring UI.
- React data-fetching refactor with unchanged presentation: frontend performance checks; no visual
  profile unless tracing reveals a user-facing change.
- Rails form validation feedback: frontend and UI craft; Emil forms and accessibility branches.
  Refactoring UI loads only if the changed feedback also affects visual hierarchy or layout.
- CSS-only spacing or typography change: Principles remains triggered; UI craft and Refactoring UI
  apply even without a language-code change.
- Keyboard-only handler fix: interface/accessibility review; no Refactoring UI visual-design load.
- Missing Emil specialist: local checks with an explicit expansion limit, not fabricated coverage.
- Missing rendered evidence for a visual judgment: pending verification, not a claimed visual pass.

These routes have not yet been validated by observing an agent's actual source-loading behavior.

Run the draft on a small library bug, a browser feature with persistence, and a multi-repository
change using project-local provisioning. Include a blocked-check case and a source change after
initial verification. Record actual commands, artifacts, reviewer findings, user interruptions, and
completion claims.

Compare fresh same-model review contexts with a single-context baseline on equivalent changes.
Evaluate missed criteria, reproduced defects, unsupported claims, and time spent. Where an
instruction's value is uncertain, repeat the scenario with and without it. This draft makes no
measured claim about perspective diversity or reliability.
