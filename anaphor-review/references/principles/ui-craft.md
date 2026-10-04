# UI craft

Read when a change affects what users see or how they interact: layout, typography, color, surfaces,
motion, controls, feedback, or responsive behavior. Trace indirect effects through callers, too. An
internal data-loading refactor with unchanged presentation stays in the frontend/language profiles.

## Choose the guidance

Read the installed `emil-ui-review` for its review method. Resolve skills by name through the host;
record the actual source path and revision or access date. These references target the Emil skill
collection supplied by the user; names alone do not establish upstream authorship or availability.

Load a specialist only when its concern changed or a concrete finding needs its detail:

- Layout, spacing, or visual priority: `emil-design-foundations`.
- Font metrics, wrapping, reading density, or numeric alignment: `emil-typography`.
- Palette, theme, or color contrast: `emil-color`.
- Elevation, borders, radii, or layered surfaces: `emil-surfaces`.
- Transitions, entry/exit behavior, gestures, or motion preferences: `emil-animations`.
- Form controls, validation, or submission feedback: `emil-forms-and-inputs`.
- Focus, input modality, target size, or accessible semantics: `emil-touch-and-accessibility`.
- Shared component interfaces or composition: `emil-component-design`.
- Paint, scrolling, large collections, or interaction latency: `emil-performance`.
- Layout stability, loading/empty states, or detailed interaction feedback: `emil-ui-polish`.

Follow `emil-ui-review`'s `STANDARDS.md` pointer only when a finding requires an exact threshold.
Avoid broad umbrella skills that recursively load the collection. If a selected skill is absent,
apply the local checks below and disclose the missing expansion under the profile procedure.

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
   overlapping Vercel, Emil, and Refactoring UI observations; multiple sources are not extra votes.

**Example:** a changed error banner pushes the focused field below the viewport and gives no route
back to it. Show the rendered state, affected field, and recovery cost; propose a scoped correction.

**Counterexample:** the existing design system uses restrained square corners. A rounder style in an
external example does not justify replacing those tokens.

Source method inspected 2026-10-04: user-supplied `emil-ui-review/SKILL.md`. Specialist rules remain
owned by their installed skills and are read only on the branches above. Missing skills are optional
expansions, not reasons to claim their rules were applied.
