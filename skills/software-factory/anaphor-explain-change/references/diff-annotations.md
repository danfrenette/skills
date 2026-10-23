# Diff annotation disclosure

Use the reader's shared Diff component for annotated source. Choose the disclosure by the reader's
task and the content it must hold. Consult the component's current contract for supported props; the
application owns source capture, identity validation, and tour schema integration.

## Choose the explanation surface

- **Inline disclosure is the default.** Use it for why the code changed, tradeoffs, failure paths,
  or explanations that readers may keep open while comparing code. Keep its numbered title visible
  and details collapsed initially. Longer rationale, lists, and small examples belong here.
- **Popover is an optional aside.** Use it for a brief, self-contained clarification, usually one
  paragraph, that readers can glance at and dismiss. For example, explain what a project-specific
  term in the code means. Its benefit is preserving code layout; its cost is temporarily covering
  nearby content. Prefer inline disclosure when the explanation needs scrolling, sustained reading,
  or comparison with another note. Include a popover only when the content benefits from it.
- **External note links locate code.** Use them when the explanation already appears in the tour.
  Activating the link reveals and highlights the original range without opening another copy of the
  explanation or moving keyboard focus. Expose hidden context inside the bounded code viewport.

Here, an inline disclosure means an expandable content region with a chevron. A dropdown menu
contains actions or choices; use it for commands, not explanatory prose. Popovers must open through
keyboard and pointer activation and support dismissal and focus return; hover is not required to
read an explanation.

## Make the target clear

Give each note one original before/after line range. Show a readable title and source-side/range
metadata, such as “Guard missing sections” and “After · L20–22”. Numbers identify notes; they are
not line numbers or an implied source-order sequence. External indexes show titles and ranges, with
a visible current-note state. Overlapping ranges retain independent explanations.

Use the same number, title, and range across the index and code annotation. Inline disclosures use a
chevron and short popover notes an information cue. Following a link locates code; activating the
annotation title opens its explanation. Keep those actions distinct.

When a range is missing from the supplied source, retain the explanation with an explicit source
unavailable state and omit its code-location action. Keep missing-source demonstrations separate
from the ordinary linked-note sequence. Consequential evidence gaps still remain visible under the
composition guide's decision-boundary rules.

## Check the reading path

Read the slice with details closed: the code, titles, and primary narrative must remain useful. Then
follow each external link and open each disclosure. Confirm the correct source side and range,
visible current state, bounded context, keyboard focus, and readable narrow-screen presentation.
These are checks of the authored content; shared component accessibility verification belongs to
component delivery. Record unavailable or unsupported reader capabilities explicitly instead of
inventing adapter fields or a parallel renderer.
