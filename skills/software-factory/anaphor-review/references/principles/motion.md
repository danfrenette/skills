# Motion review

Read when changed motion, transition lifecycle, gesture handling, or shared animation tokens affect
a user-facing surface. A static spacing or copy change does not load this profile.

## Select the depth

Read installed `review-animations` for the review method. Also read the user-supplied
`emil-animations` when available: it supplies the decision process and deeper references below.
Resolve each skill through the host and record its actual path and version or access date. The
project lock tracks the public `review-animations`; it does not represent the separate local
`emil-animations` collection as an upstream package.

Load supporting material only for the changed concern:

- A finding needs an exact threshold, easing curve, or cited rule: `review-animations/STANDARDS.md`.
- Modal, drawer, popover, tooltip, or toast behavior: the matching section of
  `emil-animations/patterns.md`, including paired backdrops and trigger-relative origins.
- Icon swaps, press feedback, list exits, or first-render behavior: the matching lifecycle section
  of `patterns.md`. Check the recipe's exception before applying a general animation rule.
- Springs, rapid reversal, gestures, or stale animation completion: the springs and interruptibility
  sections of `emil-animations/techniques.md`.
- Jitter, hover flicker, dropped frames, or theme-wide transitions: the performance and debugging
  sections of `techniques.md`. Read only the relevant implementation-stack branch.

If the local collection is unavailable, use the public review skill's applicable standards and
disclose the missing recipe coverage. A question neither source nor the local procedure can assess
remains unassessed. Do not silently substitute another skill with a similar name.

## Examine the changed interaction

1. Identify the motion's purpose, trigger, frequency, and relevant input methods. Decide whether it
   communicates useful state or delays an otherwise immediate task. Examine the existing project
   animation stack before proposing another dependency or implementation technique.
2. Trace entry, settled state, exit, and re-entry. For reversible controls, request a rapid
   open-close-open sequence; for gestures, release and reverse before settling. Check live position,
   velocity where relevant, component lifetime, and whether a stale callback changes the final
   state.
3. For grouped effects, inspect both the subject and its neighbors: backdrop synchronization, toast
   stacking, tooltip movement between siblings, icon swaps without a layout jump, and list removal
   while another item is entering. Read only the corresponding recipe.
4. Compare first render with a user-triggered transition. A fix that removes accidental startup
   motion must preserve an intentional first-run sequence. Verify keyboard and touch behavior
   separately when hover or press feedback changes.
5. Request normal-speed evidence for perceived responsiveness and a recording or slowed playback for
   suspected discontinuities. A still screenshot cannot demonstrate easing or interruption. Capture
   the revision, trigger sequence, viewport, input mode, and motion preference with the result. The
   verifier owns shared browser resources under the existing agent rules.
6. For performance claims, inspect the actual animated properties, affected subtree, and framework
   version, then request a trace under the relevant workload. A property name or library API alone
   does not prove compositor execution or dropped frames. Treat source heuristics as leads.
7. Propose the smallest correction: remove unnecessary motion, reduce it, adjust timing/origin, or
   repair lifecycle behavior before adding choreography. Return recommendations to implementation;
   this review does not edit the product.

## Resolve conflicting guidance

The inspected local `emil-animations` disables all transitions under reduced motion, while
`review-animations` permits gentler opacity/color effects. They also differ on whether an `ease-in`
exit can be appropriate. Record the conflict when it affects a finding. Apply the project's
documented accessibility and motion contract first; otherwise inspect the affected behavior and
explain the proposed choice. Neither source's blanket rule alone establishes a blocker.

Recipe exceptions matter: icon swaps, continuous progress, and gesture-driven springs need their own
rationale rather than a universal scale, curve, or duration. Use exact numbers only after checking
applicability. A meaningful unresolved product/accessibility choice goes to the owner; independent
checks can continue.

**Example:** closing and immediately reopening a drawer lets the earlier exit callback unmount the
visible panel. Cite the callback and recorded sequence; route the reachable defect to Execution and
retain the motion evidence without counting it twice.

**Counterexample:** a continuous progress indicator uses linear timing to represent elapsed time.
Replacing it with an entrance easing curve would misrepresent progress.

Report inspected states, source sections, findings, and unverified cases through the UI craft
profile. A missing required browser check follows Anaphor's verification blocker procedure; a source
review cannot stand in for that evidence. This procedure does not require an arbitrary waiting
period before delivery to satisfy a source's suggestion to revisit the motion with fresh eyes.

Local sources inspected 2026-10-04: `emil-animations/SKILL.md`, `patterns.md`, `techniques.md`, and
`review-animations/SKILL.md`. These are routing and evidence adaptations, not copies of the recipes.
