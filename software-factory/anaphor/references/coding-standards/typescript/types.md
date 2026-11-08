# Type design

Choose the narrowest type that expresses the actual contract:

1. An existing value/schema/API owns the shape: derive from it. Infer local variables and function
   results when that preserves useful information. Export a deliberate annotation when consumers
   need a stable public boundary independent of implementation details.
2. A literal/configuration object must satisfy a contract while retaining useful inferred detail:
   use `satisfies`. Use an annotation when intentional widening is the public contract; an assertion
   does not perform the same check.
3. Mutually exclusive states need different data: use a discriminated union with required fields in
   each variant. Handle every variant explicitly; use an exhaustive `never` check where a new
   variant must force callers to update.
4. A value may be absent: express that absence and narrow before use. Keep required values required
   rather than using optional properties to avoid modelling a precondition.
5. A reusable operation relates input/output types: use generics for that relation. Keep concrete
   types when there is no relationship for a generic parameter to preserve.

Keep `any`, non-null assertions, double casts, and unchecked `as` out of application contracts.
Narrow an `unknown` value, correct the producer type, or isolate a necessary interop assertion at
its boundary with an evidenced invariant and focused verification. `as const` for literal inference
is distinct from asserting unvalidated input is trusted. Keep a suppression limited to a documented
compiler/interop constraint; `@ts-expect-error` is appropriate for an intentional negative type
test.

Name types for their domain meaning. Avoid recreating the same payload shape at every layer or
turning one global `types.ts` into the owner of unrelated features. Keep generated contracts at
their generation owner and import them where needed.

Matt Pocock sources:
[unions and narrowing](https://www.totaltypescript.com/books/total-typescript-essentials/unions-literals-and-narrowing),
[annotations and assertions](https://www.totaltypescript.com/books/total-typescript-essentials/annotations-and-assertions),
and [satisfies](https://www.totaltypescript.com/how-to-use-satisfies-operator). Read the matching
section when a change introduces one of these constructs or its applicability is unclear. Record
missing material coverage rather than substituting an unsupported cast.
