# Finding requirements

Give every reviewer its assigned question, pinned baseline/head, spec or standards sources, and
access to surrounding code. Ask for:

- Changed path and line, plus the relevant caller or downstream operation.
- Requirement or documented rule when applicable; for Principles, the profile check and specific
  source or skill rule that supports it.
- Concrete trigger, reachable consequence, and evidence.
- Severity, a feasible correction, and any uncertainty that remains.

For Execution and risk passes, follow the path through inputs, state changes, and observable
outcomes. Check the actual caller before proposing a guard, retry, abstraction, or type assertion.
Reviewers may request a targeted experiment from the verifier; a speculative failure remains
unconfirmed until traced or observed.

For design concerns, identify the responsibility or caller obligation that creates the cost.
Existing legacy style does not waive a documented rule; an unrecorded preference does not become
one. Principles findings must name a concrete maintenance, testing, performance, accessibility, or
correctness cost and a proportionate alternative. Explain when the recommendation would not apply.
Check the relevant caller and framework version before recommending a language idiom. An author's
name, class length, or a formatter preference is insufficient evidence.

Report verification evidence as supplied or independently observed. Code inspection can identify a
defect without executing it, but it cannot claim a test or browser flow ran. Return a concrete
inspection limit when required source is unavailable.
