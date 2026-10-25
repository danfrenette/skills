# Finding requirements

For each claim within your assigned axis, identify the code and contract that support it, then seek
an input, caller, or responsibility boundary that would contradict it. This adversarial pass tests
the implementation independently of its author's confidence. Record supported contradictions as
findings and unresolved questions as inspection limits. Judge the builder's rationale by the same
evidence; a finding quota would reward invented objections.

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

For Standards, return a compact coverage record: applicable rule, inspected paths or symbols, and
conclusion (satisfied, violation, justified exception, or unassessed). Group related rules when they
share evidence. Explain applicability limits and cite the authority for exceptions. A finding count
alone does not establish coverage. Identify mechanical rules already enforced by repository checks;
report their actual coverage and whether results were supplied or observed.

Report verification evidence as supplied or independently observed. Code inspection can identify a
defect without executing it, but it cannot claim a test or browser flow ran. Return a concrete
inspection limit when required source is unavailable.
