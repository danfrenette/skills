# UI craft

Read when a change affects what users see or how they interact: layout, typography, color, surfaces,
motion, controls, feedback, or responsive behavior. Trace indirect effects through callers, too. An
internal data-loading refactor with unchanged presentation stays in the frontend/language profiles.

## Choose the guidance

For changed user-facing surfaces, read local `emil-ui-review` for its craft review method. Load its
`STANDARDS.md` only when a finding needs an exact threshold. Keep Anaphor's scope and evidence
rules.

Select from the globally installed [aiforui collection](https://aiforui.dev/learn/skills) below.
Resolve skills through the host and record the actual source and revision or access date.
Installation makes guidance available; select only the branches affected by the change:

- Component boundaries, composition, or shared APIs: `emil-component-design`.
- Input behavior, validation, submission, or button feedback: `emil-forms-and-inputs`.
- Tooltips, hover timers, dragging, menus, or keyboard/press behavior: `emil-interaction-details`,
  selecting its matching supporting file.
- Transitions, gestures, entry/exit behavior, or motion preferences: the [motion review](motion.md)
  branch selects `emil-animations` and its recipes and techniques by concern.
- Layout, spacing, grouping, hierarchy, or responsive ordering: the spacing and hierarchy sections
  of `emil-ui-review/STANDARDS.md`; add `emil-unslop-design` when a surface needs a design critique.
- Font metrics, wrapping, reading density, or numeric alignment: `emil-typography`.
- Palette, theme, semantic color tokens, or contrast: `emil-color`.
- Focus, keyboard/touch use, or accessible semantics: `emil-touch-and-accessibility`.
- User-facing labels, instructions, error messages, or empty-state wording: `emil-unslop-writing`,
  with `emil-forms-and-inputs` for form-specific copy.
- Shadows, borders, corners, or dark-mode depth: `emil-surfaces`.
- Icons, optical alignment, loading states, or layout stability: `emil-ui-polish`.
- Phone viewport, scrolling, safe areas, or installed web-app behavior: `emil-mobile-native`.

These are the official collection's skill names, installed separately from the public dependency
lock. Vercel's framework/performance guidance remains in the frontend profile. If an optional skill
is unavailable, use the local checks below and disclose any material coverage limit.

Anaphor owns review scope, dispatch, and the final finding disposition. Supply a specific diff and
question when reading Emil's skills so any no-question greeting branch does not interrupt the
review. Treat building/fixing instructions as recommendations in this read-only pass; return changes
to the implementation owner.

For changed visual hierarchy, spacing/grouping, typography, color emphasis, or data presentation,
also read [Refactoring UI](refactoring-ui.md). A keyboard handler fix or invisible performance
change does not need that visual-design section.

## Deeper specialists

Load these when their concern changes or an unresolved finding needs detail, not merely because the
UI method mentions their names:

- Palette derivation, tonal ramps, conversion, gamut, or contrast: `emil-color`. Select its
  conversion, scales, contrast, or gamut reference for that question. Check rendered pairs against
  the project's accessibility standard; lightness heuristics alone are not proof.
- Font capabilities, rhythm, wrapping, truncation, or text rendering: `emil-typography`. Select the
  matching reference; load its Tailwind mapping only when the project uses Tailwind.
- Rendering cost, large collections, asset loading, frame updates, layout shift, or off-screen work:
  `emil-performance`. Require relevant workload evidence for performance claims; inspect generated
  CSS and framework versions instead of assuming a utility's expansion.

Reconcile overlap with Vercel by root cause. Keep project tokens, browser support, and explicit
product decisions ahead of source defaults. Review does not authorize palette migrations, new
styling systems, or full-surface redesigns. Missing local sources follow the same disclosed coverage
limits as the other optional guidance.

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
   overlapping Vercel, Emil, and Refactoring UI observations; multiple sources are not extra votes.

**Example:** a changed error banner pushes the focused field below the viewport and gives no route
back to it. Show the rendered state, affected field, and recovery cost; propose a scoped correction.

**Counterexample:** the existing design system uses restrained square corners. A rounder style in an
external example does not justify replacing those tokens.

Official aiforui installer 0.1.7 and entitled collection inspected 2026-11-20:
[Emil Kowalski's skills](https://aiforui.dev/learn/skills). The skills own their detailed rules;
this profile owns selection and composition. Preserve their requested finding fields, adding
Anaphor's evidence and disposition fields. For stored Markdown, use labelled entries when a source's
table format would exceed the project's width rule. External approval or severity labels do not
replace Anaphor's consequence-based judgment or verification gate.
