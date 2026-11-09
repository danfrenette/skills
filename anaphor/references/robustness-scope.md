# Robustness scope

Before adding a guard, retry, lock, fallback, abstraction, or other robustness mechanism, trace the
failure through the actual callers and supported operating conditions. Apply the same procedure to
implementation choices and review recommendations; a review finding must not silently expand scope.

1. Identify the trigger, consequence, and evidence that the scenario applies. Check accepted
   requirements, documented standards, runtime topology, and existing guarantees. Describe
   likelihood from that evidence; use "unknown" when it is unknown rather than inventing a
   probability.
2. Classify the concern:
   - **Required correction:** a traced or observed defect under supported conditions, an unmet
     requirement, or an applicable documented rule violation. Implement the smallest correction and
     verify it within the agreed test boundaries. Rarity alone does not waive a required contract,
     and a source trace can establish a security defect without executing an exploit.
   - **Unresolved evidence:** applicability depends on a missing fact. Inspect the relevant source
     or request a targeted verification experiment before classifying it. If required evidence stays
     unavailable, retain the existing review and verification block; uncertainty is not permission
     to dismiss the concern or add defensive machinery.
   - **Optional hardening:** the proposal protects a hypothetical condition outside established
     requirements and supported operation, or adds protection beyond the required correction. Use
     the scope decision below before implementation.
3. Reclassify when new evidence changes the scenario. Record the evidence and disposition in the
   existing implementation brief or review findings so later workers inherit the decision.

## Scope decision

For optional hardening, check existing user authorization first. When it already covers the scenario
and complexity, proceed within that authorization and record its source. Otherwise, present:

- The concrete failure scenario and its consequence.
- Evidence for its likelihood, including assumptions and unknowns.
- The proposed protection and its implementation, maintenance, and operational costs.
- The smallest alternative, including deferral, and your recommendation.

Obtain user agreement before implementing the expansion. Continue independent accepted work while
the decision is pending. Record approval or deferral in the existing brief and carry accepted scope
into criteria and test boundaries. An optional proposal alone does not block slice acceptance or
factory delivery; required corrections and missing required evidence retain their existing gates.
This keeps the user's complexity budget explicit without weakening correctness or security checks.

For example, before proposing distributed locking for duplicate jobs, inspect queue delivery
guarantees and worker overlap. Supported redelivery that can duplicate a charge requires a
correction. Overlap possible only in an unsupported future deployment is optional hardening. Unknown
delivery guarantees require investigation before either conclusion.
