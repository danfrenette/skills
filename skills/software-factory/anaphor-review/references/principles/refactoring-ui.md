# Refactoring UI: visual design

Read only when the changed surface affects hierarchy, grouping, typography, color emphasis, or data
presentation. These local review questions are informed by Adam Wathan and Steve Schoger's
[Refactoring UI](https://refactoringui.com/), whose public contents emphasize hierarchy, spacing,
type, color, and depth. This is a scoped review baseline, not a reproduction of the book.

## Local checks

- **Hierarchy:** identify the user's next decision and compare its visual emphasis with secondary
  content in the rendered state. Flag competition only when it makes that decision harder to find.
  Prefer a scoped adjustment using existing weight, color, or spacing tokens over enlarging every
  element. Dense professional tools may intentionally expose several equally important actions.
- **Grouping:** follow labels, values, and controls through the affected responsive states. Check
  whether spacing and alignment communicate the intended relationships. Show an ambiguous grouping
  before recommending new spacing or containers; retain established density conventions.
- **Data presentation:** check whether repeated labels overpower the values people need to scan.
  Consider contextual wording or reduced label emphasis when meaning remains clear. Preserve units,
  ambiguous distinctions, and accessible form labels. The official
  [labels preview](https://refactoringui.com/previews/labels-are-a-last-resort) concerns displayed
  data, explicitly excluding forms.
- **Visual and semantic hierarchy:** assess styling separately from document structure. Adjust a
  heading's appearance without downgrading the semantics needed for navigation. Keep readable
  contrast when reducing secondary emphasis; visual quietness must not make information unusable.

**Example:** an order summary gives metadata labels more emphasis than the total and payment action.
Show how that ordering interferes with checkout, then propose a token-level hierarchy adjustment.

**Counterexample:** a dense audit table uses explicit repeated labels to disambiguate similar
values. Removing them to make the page look cleaner would reduce comprehension.

## Evidence limits

Use the UI craft profile's rendered-evidence requirements and Anaphor's finding severity. Preserve
the accepted design and product scope. Consult additional official previews or user-provided book
material only when the changed concern needs them; report unavailable detail instead of inventing a
book rule. Do not substitute an unattributed third-party skill for the authors' guidance.

Public source pages checked 2026-10-04. These questions are Anaphor's adaptations; the full book has
not been loaded or evaluated as part of this profile.
