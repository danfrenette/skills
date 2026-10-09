# JavaScript and TypeScript

Read for changed JavaScript/TypeScript logic, public interfaces, state models, or tests. Kent C.
Dodds informs behavior-focused testing; Matt Pocock informs type design and inference. Apply
[Frontend](frontend.md) as well when browser behavior or rendering changes.

## Tests observe the user-facing contract

**Trigger:** a test is added or its mocks, assertions, or interaction path change.

Identify the consumer: an end user, an API caller, or a developer using the exported interface. Ask
whether a broken interaction could pass because the test calls a private handler or asserts internal
state directly. Also ask whether an equivalent internal refactor would break it. Show the omitted
behavior and propose an assertion through the agreed public test boundary. Internal isolation can
support diagnosis; it does not replace evidence for the public outcome. Sources: Kent C. Dodds's
[Testing Implementation Details][testing] and [testing-layer tradeoffs][layers].

Read installed Matt Pocock `tdd` for its test-quality rules; this is a review of the resulting
tests, not a restart of its implementation loop. If test-seam design is the concern, read
`codebase-design`.

## Types reflect validated states

**Trigger:** external data, nullable values, unions, assertions, `any`, or non-null assertions
change.

Trace where a value becomes trusted and which control-flow branch justifies its use. A cast alone
does not check runtime input. Flag a hidden invalid state only with a plausible incoming value and
consumer. When booleans and optional fields describe mutually exclusive states, consider a
discriminated union that lets callers narrow those states. A local assertion backed by an inspected
invariant need not become a new validation layer. Sources: Matt Pocock's [Unions, Literals, and
Narrowing][narrowing] and [Annotations and Assertions][assertions].

## Preserve useful inference

**Trigger:** an annotation widens literals or an assertion suppresses checking of a configuration or
mapping object.

Show which caller loses precision or which invalid member escapes checking. Consider `satisfies`
when the object needs shape validation while retaining inferred information; use an annotation when
the wider public contract is intentional. Require a supported compiler version. A stylistic
preference for one syntax is not a finding. Source: Matt Pocock's [satisfies examples][satisfies].

## Loading more guidance

Consult relevant sections of the installed disciplines and linked primary sources when expanding a
check. TypeScript rules do not justify migrating an untyped JavaScript project. For Node-only
changes, omit browser/React rules; for React or Next.js changes, use the framework branch in the
frontend profile. Record missing source coverage under the [Principles procedure](README.md).

Primary sources checked 2026-10-04:

[testing]: https://kentcdodds.com/blog/testing-implementation-details
[layers]: https://kentcdodds.com/blog/static-vs-unit-vs-integration-vs-e2e-tests
[narrowing]:
  https://www.totaltypescript.com/books/total-typescript-essentials/unions-literals-and-narrowing
[assertions]:
  https://www.totaltypescript.com/books/total-typescript-essentials/annotations-and-assertions
[satisfies]: https://www.totaltypescript.com/how-to-use-satisfies-operator
