# UI craft

Read when a change affects what users see or how they interact: layout, typography, color, surfaces,
motion, controls, feedback, or responsive behavior. Trace indirect effects through callers, too. An
internal data-loading refactor with unchanged presentation stays in the frontend/language profiles.

## Choose the guidance

Select from the project-locked sources below. Resolve skills through the host and record the actual
source and revision or access date. Installation makes guidance available; it does not load every
skill into every review. Select only the branches affected by the change:

- Interaction feedback, component behavior, or polish requiring design-engineering judgment: Emil
  Kowalski's `emil-design-eng`. Read the sections for that concern rather than expanding its entire
  set of topics into the review brief.
- Transitions, gestures, entry/exit behavior, or motion preferences: Emil's `review-animations`.
  Load its `STANDARDS.md` only when a finding needs a precise value or citation.
- Layout, spacing, grouping, or responsive ordering: Jakub Krehel's `better-layout`.
- Font metrics, wrapping, reading density, or numeric alignment: `better-typography`.
- Palette, theme, semantic color tokens, or contrast: `better-colors`.
- Focus, keyboard/touch use, accessible semantics, or form accessibility: `better-accessibility`.
- User-facing labels, instructions, error messages, or empty-state wording: `better-writing`.
- Surfaces, icons, optical alignment, loading states, or layout stability: `better-ui`. Follow its
  supporting-file pointers only for affected concerns; its animation guidance need not repeat a
  completed `review-animations` pass.

These names refer to `emilkowalski/skills` and `jakubkrehel/skills`, as recorded by the lock. The
previous user-supplied `emil-*` collection is not an alias for those public skill names. Vercel's
framework/performance guidance remains in the frontend profile. Use the local checks below when an
optional source is missing, disclosing any material coverage limit.

Anaphor owns review scope, dispatch, and the final finding disposition. Do not invoke Jakub's
`better-interface` or `interface-review` wrappers as an additional orchestration layer. Supply a
specific diff and question when reading Emil's skills so their no-question greeting branch does not
interrupt the review. Treat building/fixing instructions as recommendations in this read-only pass;
return changes to the implementation owner.

For changed visual hierarchy, spacing/grouping, typography, color emphasis, or data presentation,
also read [Refactoring UI](refactoring-ui.md). A keyboard handler fix or invisible performance
change does not need that visual-design section.

## Local checks and reporting adaptations

1. Name the affected task, state, and input method. Trace whether the user can locate the action,
   operate it, recognize its result, and recover from failure. This grounds craft findings in use.
2. For visual or timing judgments, inspect revision-matched rendered evidence at the affected
   viewport and state. Source can prove a missing label; it cannot prove a balanced composition or
   comfortable animation. Request missing browser evidence from the verifier and distinguish pending
   evidence from observed defects. Required checks retain Anaphor's verification gate.
3. Compare the changed surface with the project's design system and nearby unchanged components.
   Explain the specific loss of clarity, consistency, stability, or feedback. A preference for
   another aesthetic is insufficient grounds for a finding or redesign.
4. Treat the external skill's numerical defaults and flag-on-sight rules as investigation prompts.
   Check framework behavior, input needs, and the project's adopted accessibility standard before
   assigning severity. Author taste is not automatically a standards violation.
5. Preserve source anchors, then report through Anaphor's finding fields and dispositions. An
   external "Ship it" verdict cannot bypass verification or change draft-PR delivery. Deduplicate
   overlapping Vercel, Emil, Jakub, and Refactoring UI observations; multiple sources are not extra
   votes.

**Example:** a changed error banner pushes the focused field below the viewport and gives no route
back to it. Show the rendered state, affected field, and recovery cost; propose a scoped correction.

**Counterexample:** the existing design system uses restrained square corners. A rounder style in an
external example does not justify replacing those tokens.

Official skill definitions inspected 2026-10-04:
[Emil Kowalski](https://github.com/emilkowalski/skills) and
[Jakub Krehel](https://github.com/jakubkrehel/skills). The skills own their detailed rules; this
profile owns selection and composition. Preserve their requested finding fields, adding Anaphor's
evidence and disposition fields. For stored Markdown, use labelled entries when a source's table
format would exceed the project's width rule. External approval or severity labels do not replace
Anaphor's consequence-based judgment or verification gate.
