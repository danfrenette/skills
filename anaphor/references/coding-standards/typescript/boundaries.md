# Boundary contracts

For each value entering from HTTP, storage, a provider, or user input, identify the runtime check
that establishes its contract. Treat unvalidated values as `unknown`; parse with the project's
existing validator and pass the validated value inward. Reuse that contract rather than adding
speculative checks to every internal consumer. A static type does not authenticate or authorize a
caller.

Derive transport types from the authoritative schema or API, with only the fields the consumer is
allowed to receive. Keep database-only fields and server imports behind the boundary. At JSON or
other serialization steps, account for representation changes explicitly: a TypeScript brand or
assertion neither validates the received payload nor revives dates or other runtime objects.
Existing generated/end-to-end tools are contract owners, not reasons to replace the project's API
stack.

Selected adaptations from Rhys Sullivan's
[quality-code](https://github.com/RhysSullivan/skills/blob/main/skills/quality-code/SKILL.md):

- Brand primitives when distinct domain values could be confused. Validate at construction and use
  existing branding primitives when available; a brand alone supplies no runtime check.
- Derive shared shapes with inference/utility types from their owner. Keep explicit public transport
  contracts when persistence and exposure differ.
- Prefer named option objects for application operations with several arguments. Preserve public
  positional APIs and measured hot-path requirements.
- For validator-neutral library APIs, consider Standard Schema compatibility when accepting caller
  validators is an actual requirement; keep the application's existing validator otherwise.

The type-design reference owns discriminated-state modelling. These are scoped adoptions, not a
requirement to brand every string, add validation dependencies, or change frameworks.
