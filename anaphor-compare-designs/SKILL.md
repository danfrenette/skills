---
name: anaphor-compare-designs
description:
  Compare implementation alternatives when an accepted spec leaves competing interfaces, ownership
  models, or failure behavior unresolved.
---

# Anaphor: compare designs

Settle one implementation decision while preserving the accepted product behavior. Use
[agent handoffs](../anaphor/references/agents.md) for isolated contexts and ownership.

1. State the decision, accepted criteria, applicable standards, behavior to preserve, and baseline.
   If the disagreement is a product requirement, return that question to the user before comparing
   implementations.
2. Define two or three alternatives that differ in a concrete constraint: where a decision belongs,
   what callers must know, or how failures propagate. Give every candidate the same requirements and
   standards. Read installed `codebase-design` and its `DESIGN-IT-TWICE.md` when interface or seam
   placement is the question.
3. Choose observable comparison criteria before generation: caller obligations, reachable failure
   cases, migration steps, and behavior-test results. Require standards and acceptance compliance
   from every candidate; alternatives cannot gain points by omitting requirements.
4. Give each candidate a fresh context and the same baseline. For source-level designs, request
   interfaces, caller examples, and a traced scenario. Build the smallest experiment when source
   reasoning cannot settle the question; read installed `prototype` for that disposable experiment.
   Keep the accepted spec fixed and record the answer before returning to implementation. Isolate
   writable experiments; obtain runtime resources through project setup instructions only when
   needed.
5. Inspect alternatives without sharing one candidate's rationale with another. Label results A/B/C
   and compare their evidence against the declared criteria. Resolve a factual disagreement with a
   test or source trace. Agreement alone does not select a winner.
6. Select one coherent design and record the decision, rejected tradeoffs, and evidence in the
   brief. Integrate useful parts deliberately. Return production implementation to Anaphor's
   [implementation procedure](../anaphor/references/implementation.md); experiment code has not
   passed its delivery gates.

**Done:** the implementation decision is supported by observed or traced evidence, the selected
design satisfies the shared constraints, and candidate changes are accounted for. Preserve
experiments until their useful work and evidence are captured.
