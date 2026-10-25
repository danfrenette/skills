---
name: anaphor-review
description:
  Review a change through separate Standards, Spec, and language-specific Principles agents, with
  execution and risk passes for changed runtime behavior.
---

# Anaphor: review

Read Matt Pocock's installed `code-review` and [agent handoffs](../anaphor/references/agents.md)
before dispatch. Supply the accepted spec and original baseline directly; use tracker discovery only
to retrieve missing requirements. Preserve its Standards/Spec separation and labelled smell
heuristics, adding the Principles and triggered Execution/risk passes below. Review is read-only;
findings return to the implementation owner.

## Pin the review

Resolve the supplied baseline and head in each repository. Review committed changes from their
merge-base; record both revisions and the commits covered. For a remote PR, capture its base and
head and retrieve surrounding source and standards at that head. Recheck the head before reporting;
changed contents require affected review again.

Include the accepted spec, testing decisions, applicable repository standards, and evidence
references. An empty change has nothing to review. If requirements or a valid baseline are missing,
name that limit; an unassessed Spec axis cannot satisfy Anaphor's delivery gate.

## Select the passes

- **Standards — every review:** which documented rules does the change violate? Label smell
  heuristics separately.
- **Spec — every review:** which accepted requirements are missing, incorrect, partial, or exceeded?
- **Principles — source, tests, or user-facing presentation changes:** which language/framework
  idioms, responsibilities, abstractions, or test designs create a concrete cost? Include templates,
  styles, and visual assets; mark internal documentation-only changes not applicable with a reason.
  Load [Principles procedure and profiles](references/principles/README.md) in that reviewer's
  context.
- **Execution — runtime logic, interfaces, persisted state, or integrations change:** which
  reachable caller, state transition, or failure path breaks the intended contract?
- **Security — identity, access, secrets, trust boundaries, or untrusted input changes:** can an
  input reach a sensitive operation without its required control?
- **Concurrency — multiple writers, retries, background work, or ordering changes:** what happens
  under overlap, repetition, and partial failure?
- **Migration — stored representations, compatibility, or rollout changes:** do supported old/new
  states and deployment orders preserve the contract?
- **Performance — query shape, hot loops, request fan-out, or resource bounds change:** which
  realistic workload exceeds the intended cost or resource limit?

Assign Standards, Spec, and Principles to separate fresh, read-only subagents. The Principles agent
owns all applicable language profiles and reports coverage for each; mixed-language changes must
cover each changed surface. Give it changed paths and behavior, not preloaded profile contents.
Standards and Spec do not need the Principles source library in their briefs. Apply the handoff
rules for model selection and limited concurrency. Execution and risk passes receive their own
questions and sources. Read [finding requirements](references/findings.md) before assigning any
pass.

## Judge and report

Check the recorded reviewer isolation and Standards coverage before accepting the reports.
Return missing applicable rule assessments to the assigned reviewer; treat them as unassessed
until evidence is supplied. Report reduced context separation independently of finding counts.

Trace each proposed finding through the changed path. A reproduced failure, reachable correctness
defect, applicable standards violation, unmet criterion, or exposed security issue blocks
completion. A design preference needs a concrete cost and remains a labelled judgment.

For each finding, record act on, consider, noted, or dismissed, with its evidence and owner. Explain
dismissals against the actual path or rule. Report **Standards**, **Spec**, and **Principles** as
three separate axes, each with its findings, count, and evidence limits. Within Principles, group
results by language/framework and identify the profiles and sources applied. Give Execution and risk
passes their own results. Cross-reference duplicate concerns under their owning axis without
counting them again or turning votes into confidence scores. An external author's preference alone
does not block delivery; a traced defect or documented rule breach can.

**Done:** the report identifies the reviewed revisions, executed passes, findings and dispositions,
and evidence limits. A triggered pass that cannot inspect its required source remains unassessed and
prevents factory delivery. No findings means no findings within that inspected scope, not proof that
runtime verification passed.
