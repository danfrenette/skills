# Rails results and failures

## Establish the result contract

Inspect the existing service base, result API, and callers before changing them. Preserve supported
contracts; the sample below describes Autodidact's custom API, not a Rails built-in. Where the
project already uses a different result mechanism, retain its public contract and apply named
outcomes, explicit sequencing, safe failures, and ownership through that mechanism.

For a new application adopting this sample contract:

- `ApplicationResult` owns common `success`, `errors`, and `error_code` fields and status
  predicates. Use `ApplicationResult.define(:source)` or another named business payload. Operations
  may share a named feature result only when payload and outcome meanings match. Generic `value`
  payloads or unrelated fields in one result hide the caller's contract.
- Feature results used by endpoints own `http_status`; the common base stays free of feature status
  policy. Keep requests, rendering, and persistence out of results. Pass semantic codes using
  `error_code:` and expose deliberate user-safe errors.
- Supply named payload keywords on success and failure, usually `nil` on failure. In the original
  custom implementation, payload readers are not Ruby `Data` members: inherited `to_h` and equality
  include only common fields. Read payloads explicitly at serialization boundaries and preserve the
  chosen behavior in compatibility tests.
- The application service base owns common `NotFound` and `InvalidInput` exception types. Use cases
  own their user-scoped lookups and required-value checks; feature exceptions name additional
  business failures.

Implement and test the base API before building callers that assume it exists. Preserve established
helpers rather than adding a result/monad dependency solely to restate the same contract.

## Separate expected failure from defects

Concrete instance `call` methods rescue expected business exceptions and return failures with
explicit safe messages. Rescue specific persistence/provider exceptions only when their business
meaning is understood. Arbitrary exception messages are not product copy.

For a base adopting the Rails sample's error policy, inherited class `.call` dispatches to
`new(...).call`, reports unexpected `StandardError`, and re-raises the original exception with its
backtrace. Rails handles the generic HTTP 500. Expected returned failures are not unhandled events.
A direct instance call bypasses that class wrapper; use and test the intended public entry point.

Coordinate nested wrappers and framework instrumentation so a propagated exception is reported once.
Reporter failure must preserve the original exception. Use the project's selected reporter and
sanitized operational context; credentials, cookies, tokens, and private user content stay out of
events. Verify actual event delivery and duplicate suppression when reporting integration changes.
This sample authorizes no telemetry provisioning or vendor switch.

## Stop failed sequences

Inspect each child result before dependent work. Neither a failure return nor an error-reporting
wrapper implies short-circuiting, recovery, or database rollback. Follow
[persistence](persistence.md) for atomic writes and test failure after an earlier successful step.
