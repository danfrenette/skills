# Content composition

Organize the explanation around what the reader needs to understand and assess. Matt Pocock's `pr`
informs the summary, before/after evidence, and reversibility questions; this procedure extends
those ideas to detailed walkthroughs. A short PR body introduces the tour. The tour opens with
linked business cases, then develops each case through implementation slices and evidence, with
deeper scenarios, diagrams, graphs, and receipts available on demand.

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

Open with a concise list of business cases. Each item states who benefits and what improves, then
links to its detailed section through a stable anchor. Define unfamiliar terms only when needed.
This summary should help the owner choose a question to investigate.

Give each case a short summary for its contents card and a clear before/after account for its
chapter. Keep case and step titles distinct enough to navigate in the sidebar or narrow menus.
End each case before starting the next; supporting details must not obscure that boundary.

Organize detailed sections by business case. State the changed behavior before and after, then
follow the implementation from its entry point to its observable result. A case may need several
vertical code slices across multiple files; group them by the claim they explain rather than by file
or implementation layer. Put useful pinned code beside the claim, with original file line numbers
and concise authored annotations explaining consequential decisions and failure paths. Preserve full
source context inside bounded scroll windows.

Place evidence beside the claim it supports. Show what was observed and what that observation
establishes. Keep requirements, deeper decisions, source revisions, execution receipts, and history
in supporting disclosures. Keep open concerns visible within the affected case. End with concerns
that affect the PR as a whole, including dependencies, rollout, and rollback consequences. Cases
remain directly accessible; reading them in order is optional.

When choosing inline explanations, short popovers, or external code links, follow
[Diff annotation disclosure](diff-annotations.md).

Write annotations and captions in simplified technical English: use a clear subject, an active verb,
and familiar project terms. State one main idea at a time. Explain why the selected code matters;
let the code show the mechanics. Use STE-informed writing without claiming formal ASD-STE100
compliance.

Keep the main path readable without opening external links. Put pinned source URLs and revisions,
spec criteria, deeper rationale, acceptance details, receipts, and execution history behind the
reader's design-system disclosures. Keep consequential failures and missing required evidence
visible at the decision boundary. Supporting detail remains available; disclosure changes its
prominence, not its provenance or completeness.

Write each case's verification as a short story: what needed proof, how the check worked, and what
the evidence supports. Use the reader's optional verification purpose, method, and conclusion.
Connect that story to the original checks and receipts. State source limits and unrun checks
explicitly. Use one flat Verification details panel for the requirement, action, result,
environment, source, assessments, and receipts. Give requirements descriptive names; explain IDs
such as T1 as references to the linked specification. Environment icons describe only browsers
named by the recorded run. Keep context and source available without nested disclosures.

Audit the authored reading path against ASD-STE100: short sentences, one topic per paragraph,
consistent technical names, and approved word meanings. Record the rules checked and any limits.
A sentence-length screen alone does not verify the dictionary or full compliance. Preserve original
historical evidence and quoted source wording; distinguish these from the new authored explanation.

Review the summary links and each case with supporting details closed. Remove prose that repeats an
annotation, code, or capture. A slice without useful code may lead with its observed artifact or
short explanation; nonvisual changes still need evidence and a clear connection to the changed
source.

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

Check that every summary item reaches its business case, each case connects changed behavior to code
and evidence, and open concerns remain visible. Each annotation must add needed understanding, each
visual must answer a reader question, and each verification claim must have an accessible receipt.
For local preview checks, follow
[launch and inspect locally](anaphor-integration.md#launch-and-inspect-locally). The PR body should
summarize the changed behavior, link decisive evidence, identify concrete risks, and point to the
relevant tour section. Local preview links are explicitly for the current machine; share hosted
links with external readers when publication is requested.
