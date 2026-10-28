# Ruby services and ownership

## Define the operation

Expose one public instance operation, `call`, through the project's class-level `.call` dispatcher.
Initializers store explicit dependencies and inputs; run business work, process launches, network
requests, and environment discovery during the operation so construction has no external effects.
Required preconditions stay required inputs; [arguments](arguments.md) owns optionality decisions.

Keep business steps private and name them for the operation they perform. A simple use case stays in
one service. Extract a focused service only when it owns a separate responsibility; a parent then
coordinates its results. Namespace by capability and use operation names rather than `Manager`,
`Processor`, or `Utils` buckets.

Choose the orchestration shape for the selected profile:

- **Rails:** aim for roughly five lines of business steps in instance `call`, excluding rescue and
  necessary control flow. A step can return a result, but the parent must inspect it and stop on
  failure. The endpoint's [result policy](../rails/results.md) owns expected/unexpected errors.
- **Ruby library:** business-operation `call` contains bareword private step calls, one per line.
  Put arguments, receivers, assignments, conditions, loops, blocks, explicit returns, and result
  construction inside private steps. The final step returns the result. Rescue clauses may map
  expected exceptions to the library's established failure contract. Shared dispatchers and
  low-level value/protocol helpers are outside this business-orchestration rule.

A private step returning failure does not stop later steps. Under bareword orchestration, raise a
meaningful exception handled by the service or existing command boundary when a prerequisite fails.
Inspect child-command results inside the owning step before dependent work. Keep resource
acquisition/use/cleanup in one private scope; adding instance state just to divide that scope loses
its lifetime guarantee.

## Assign behavior to its owner

Tell, don't ask: invoke the known collaborator's operation instead of branching on `is_a?`,
`kind_of?`, or `respond_to?`. Apply the same rule to in-process validation. Validate business facts
and use a shared interface or focused external adapter. At an untrusted boundary, validate the real
protocol and required data before passing a stable value inward.

Use size as a responsibility signal, not an extraction quota. Five-line methods, 100-line classes,
and four parameters are review heuristics; count independent keyword options. The Rails source's
service-constructor smell threshold is more than five independent inputs. Explain exceptions by
cohesion and caller obligations; hiding options in a hash changes neither. An input object earns its
place through cohesive behavior or invariants.

## Express intent in code

Application code expresses intent through names, small methods, and clear owners. Keep explanatory
prose in owning documentation or the change description; preserve functional directives such as
`# frozen_string_literal: true`. Fixture provenance and verification instructions belong with tests
and recipes.

Use `tap` when configuring and returning the same object, `each_with_object` when accumulating into
a mutable collection, and `map` for one-to-one transformations. With `each_with_object`, mutate the
accumulator instead of reassigning its block variable. Keep locals that explain or reuse an
intermediate value; replace locals used solely to initialize, mutate, and return an object. These
blocks live inside private steps under the Ruby-library orchestration rule.
