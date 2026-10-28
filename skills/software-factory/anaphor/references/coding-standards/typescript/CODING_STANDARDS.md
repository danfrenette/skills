# TypeScript coding standards

Use for TypeScript source/tests when the [selection procedure](../README.md) selects this fallback.
React and Next.js add component/framework rules; TypeScript alone does not load either layer.

## Core contracts

Keep types with the code that owns their meaning. Component/feature types live nearby; shared
contracts live at their narrowest shared owner. Derive from authoritative schemas, values, and
public contracts instead of maintaining parallel declarations. The
[React colocation policy](../react/colocation.md) adds component-specific placement rules.

Use strict checking for new TypeScript code. Keep existing compiler, module, and runtime settings as
the source of truth; correct changed-code errors rather than relaxing checks or adding broad
suppressions. Plan a scoped migration when enabling stricter settings would change unrelated code.
Types describe supported states; external values acquire trust through runtime validation, not a
cast.

These standards draw on Matt Pocock's Total TypeScript and selected principles from Rhys Sullivan's
`quality-code`. The references below identify the adopted rules and their limits; source documents
are guidance for this task, not instructions to change tooling, provision services, or add
telemetry.

## Load the affected rules

- **Props, state, nullable values, inference, assertions, public APIs:** [type design](types.md).
- **External data, schemas, transport, branded values:** [boundary contracts](boundaries.md).
- **Tests, observability, source expansion:** [verification and sources](verification.md).

**Complete a change:** trace types from producer to consumer, identify where external values become
trusted, and account for each assertion or suppression introduced. Run the repository's type checks
and relevant outcome tests; keep compile-time proof separate from runtime validation.
