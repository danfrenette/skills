# Content composition

Organize the explanation around what the reader needs to understand and assess. Matt Pocock's `pr`
informs the summary, before/after evidence, and reversibility questions; this procedure extends
those ideas to detailed walkthroughs. A short PR body introduces the tour. The tour develops each
vertical slice through code and annotations, with deeper scenarios, diagrams, graphs, and evidence
available on demand.

## Plan the explanation

Identify the audience and the questions the change raises: what the user experiences, how the system
produces that result, why the design was chosen, what was exercised, and what could go wrong. Use
the request and accepted spec to set depth. Ask only when an unresolved audience or publication
constraint would materially change the artifact.

Make a working outline that pairs each important question with its scenario, source/code pointers,
and available evidence. Reuse the implementation brief and receipts. Missing evidence remains an
explicit limit; route a new verification need to `anaphor-verify` when authorized. An explanation
cannot manufacture the observation it needs.

## Compose the main reading path

Open with a short business case: who has the problem, why it exists, and what this PR changes for
that person. Define only unfamiliar terms needed to understand the slices that follow. The opening
should prepare the reader to inspect code rather than repeat the implementation plan.

Order the primary vertical slices as one linear journey from entry point to observable outcome. Put
captured code directly after each slice heading. Use the actual pinned before/after source, original
file line numbers, and a few authored ranges. Put the explanation beside the relevant lines. Use one
or two short sentences per annotation to explain the consequential behavior or decision. Include
important failure paths. Preserve full source context for inspection inside bounded scroll windows;
following an annotation must not expand the whole file into the page.

Write annotations and captions in simplified technical English: use a clear subject, an active verb,
and familiar project terms. State one main idea at a time. Explain why the selected code matters;
let the code show the mechanics. Use STE-informed writing without claiming formal ASD-STE100
compliance.

Keep the main path readable without opening external links. Put pinned source URLs and revisions,
spec criteria, deeper rationale, acceptance details, receipts, and execution history behind the
reader's design-system disclosures. Keep consequential failures and missing required evidence
visible at the decision boundary. Supporting detail remains available; disclosure changes its
prominence, not its provenance or completeness.

Review the flow once with supporting details closed. Remove prose that repeats an annotation, code,
or capture. A slice without useful code may lead with its observed artifact or short explanation;
nonvisual changes still need evidence and a clear connection to the changed source.

## Select visuals by the question

Use the smallest useful visual for each question. Several focused visuals can support a detailed
tour; one crowded diagram should not have to explain the entire change.

- **Who owns what?** Use a component or dependency diagram, or a shallow file tree with
  responsibilities. Show boundaries and label relationships.
- **What happens in what order?** Use a sequence diagram or call tree, including meaningful
  asynchronous work and failure paths.
- **Which states and transitions matter?** Use a state diagram or before/after flow. Include the
  conditions that permit or reject transitions.
- **What logic changed?** Use a captured, pinned diff with concise annotations. Use pseudocode only
  when it explains something the real code cannot show clearly, and label it illustrative.
- **What does the user see?** Use screenshots or a recording from the observed flow, with the
  relevant action, role, and result explained.
- **How does behavior vary with load, time, or another quantity?** Use a graph from measured data.
  Identify axes, units, workload, collection method, and tested revision. Label hypothetical
  examples as illustrative and keep them separate from verification evidence.

Use diagrams supported by the reader, or import an accessible rendered artifact alongside its
source. For measured graphs, retain the data and generation method.

Place each visual beside the code or claim it supports. Use a short caption for the observed state
or action and result; keep its source, scope, and receipt available in supporting details. Use
readable labels and provide a textual account of the important relationship or result. Check
rendering and links in the intended surface when available; disclose an unverified rendering instead
of claiming it was inspected.

## Connect claims to observations

For each important behavioral claim, connect the scenario to an executed check and its observed
result. Include before/after evidence when available, especially a regression's failing and passing
test. Distinguish an observed baseline from a description inferred from source. Never invent a
before screenshot or imply that an unexecuted old revision was tested.

Diagrams describe behavior and structure; verification receipts establish what was exercised.
Screenshots demonstrate visible states; they do not by themselves establish persistence,
authorization, or other unobserved effects. Link the relevant runtime or test evidence for those
claims. Explain what each result establishes and its limits, preserving revisions and provenance
under the parent skill's evidence rules.

## Explain consequences and hand off

Describe affected users, consumers, stored data, and cross-repository dependencies where relevant.
Explain whether reverting the code restores the previous behavior, or whether data changes, external
effects, or rollout order require additional recovery. State unknowns using the available decision
record and evidence; a one-word risk label is insufficient.

Check that the business case leads directly into the code-led slices, each annotation adds needed
understanding, each visual answers a reader question, and each verification claim has an accessible
receipt. For local preview checks, follow
[launch and inspect locally](anaphor-integration.md#launch-and-inspect-locally). The PR body should
summarize the changed behavior, link decisive evidence, identify concrete risks, and point to the
relevant tour section. Local preview links are explicitly for the current machine; share hosted
links with external readers when publication is requested.
