# Content composition

Organize the explanation around what the reader needs to understand and assess. Matt Pocock's `pr`
informs the summary, before/after evidence, and reversibility questions; this procedure extends
those ideas to detailed walkthroughs. A short PR body introduces the document. The document can
develop multiple scenarios, diagrams, and graphs without inheriting the PR template's brevity.

## Plan the explanation

Identify the audience and the questions the change raises: what the user experiences, how the system
produces that result, why the design was chosen, what was exercised, and what could go wrong. Use
the request and accepted spec to set depth. Ask only when an unresolved audience or publication
constraint would materially change the artifact.

Make a working outline that pairs each important question with its scenario, source/code pointers,
and available evidence. Reuse the implementation brief and receipts. Missing evidence remains an
explicit limit; route a new verification need to `anaphor-verify` when authorized. An explanation
cannot manufacture the observation it needs.

Lead with the changed experience and a map of the explanation. Develop scenarios in reader order:
entry point, important responsibilities, state changes, observable outcome, then relevant failure
paths. Explain domain terms before implementation details. Add cross-repository and design detail
where it answers a question, with links to pinned source and recorded decisions.

## Select visuals by the question

Use the smallest useful visual for each question. Several focused visuals can support a detailed
document; one crowded diagram should not have to explain the entire change.

- **Who owns what?** Use a component or dependency diagram, or a shallow file tree with
  responsibilities. Show boundaries and label relationships.
- **What happens in what order?** Use a sequence diagram or call tree, including meaningful
  asynchronous work and failure paths.
- **Which states and transitions matter?** Use a state diagram or before/after flow. Include the
  conditions that permit or reject transitions.
- **What logic changed?** Use a small diff sketch or pseudocode. Label illustrative code and link
  the actual implementation.
- **What does the user see?** Use screenshots or a recording from the observed flow, with the
  relevant action, role, and result explained.
- **How does behavior vary with load, time, or another quantity?** Use a graph from measured data.
  Identify axes, units, workload, collection method, and tested revision. Label hypothetical
  examples as illustrative and keep them separate from verification evidence.

Prefer Mermaid for static software diagrams supported by the publishing surface. For measured
graphs, retain the data and generation method with an accessible rendered artifact. Use an
interactive format only when requested or supported by the delivery contract; the durable document
must remain understandable without a local development server.

Place each visual beside the explanation it supports. Caption what it shows, its scope, and the
source or receipt behind it. Use readable labels and provide a textual account of the important
relationship or result. Check rendering and links in the intended surface when available; disclose
an unverified rendering instead of claiming it was inspected.

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

## Explain consequences and publish

Describe affected users, consumers, stored data, and cross-repository dependencies where relevant.
Explain whether reverting the code restores the previous behavior, or whether data changes, external
effects, or rollout order require additional recovery. State unknowns using the available decision
record and evidence; a one-word risk label is insufficient.

Check that the overview leads to the detailed scenarios, each visual answers a reader question, and
each verification claim has an accessible receipt. The PR body should summarize the changed
behavior, link decisive evidence, identify concrete risks, and point to the full walkthrough.
