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
heuristics, adding the Principles and triggered Execution/risk passes below. Use the host's agent
mechanism and inherited model under the handoff rules. Review is read-only; findings return to the
implementation owner.

## Pin the review

Resolve the supplied baseline and head in each repository. Review committed changes from their
merge-base; record both revisions and the commits covered. For a remote PR, capture its base and
head and retrieve surrounding source and standards at that head. Recheck the head before reporting;
changed contents require affected review again.

Include the accepted spec, testing decisions, applicable repository standards, and evidence
references. An empty change has nothing to review. If requirements or a valid baseline are missing,
name that limit; an unassessed Spec axis cannot satisfy Anaphor's delivery gate.

## Select the passes

- **Pass:** Standards

  **Trigger:** Every review

  **Question:** Which documented rules does the change violate? Label smell heuristics separately.

- **Pass:** Spec

  **Trigger:** Every review

  **Question:** Which accepted requirements are missing, incorrect, partial, or exceeded?

- **Pass:** Principles

  **Trigger:** Source code, tests, or user-facing presentation changes, including templates, styles,
  and visual assets. Mark internal documentation-only changes not applicable with a reason.

  **Question:** Which language or framework idioms, responsibility choices, abstractions, or test
  designs create a concrete cost in this change? Read the
  [Principles procedure and profiles](references/principles/README.md) in that reviewer's context.

- **Pass:** Execution

  **Trigger:** Runtime logic, interfaces, persisted state, or integration behavior changes

  **Question:** Which reachable caller, state transition, or failure path breaks the intended
  contract?

- **Pass:** Security

  **Trigger:** Identity, access checks, secrets, trust boundaries, or untrusted input changes

  **Question:** Can a concrete input reach a sensitive operation without its required control?

- **Pass:** Concurrency

  **Trigger:** Multiple writers, retries, background work, or ordering changes

  **Question:** What happens under overlap, repetition, and partial failure?

- **Pass:** Migration

  **Trigger:** Stored representations, compatibility, or rollout transitions change

  **Question:** Do supported old/new states and deployment orders preserve the contract?

- **Pass:** Performance

  **Trigger:** Query shape, hot loops, request fan-out, or resource bounds change

  **Question:** Which realistic workload exceeds the intended cost or resource limit?

Assign Standards, Spec, and Principles to separate fresh, read-only subagents. The Principles agent
owns all applicable language profiles and reports coverage for each; mixed-language changes must
cover each changed surface. Give it changed paths and behavior, not preloaded profile contents.
Standards and Spec do not need the Principles source library in their briefs. Use the inherited
model for every agent, running sequential fresh contexts when concurrency is limited under the
[handoff rules](../anaphor/references/agents.md). Execution and risk passes receive their own
questions and sources. Read [finding requirements](references/findings.md) before assigning any
pass.

## Judge and report

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
