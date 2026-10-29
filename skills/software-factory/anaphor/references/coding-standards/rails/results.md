# Rails results and failures

## Define the caller's outcomes

Inspect the existing service base, result API, and callers before changing them. Retain the shared
infrastructure and supported public contracts. For each changed operation:

1. List the decisions its callers must make after execution. Creation, updating an existing record,
   and rejection may need distinct outcomes even when two are successful.
2. Give each outcome explicit semantics and named data. Use the existing result mechanism to expose
   an outcome code or predicates; define which combinations are valid so callers cannot observe
   contradictory states. Keep user-safe errors explicit.
3. Return enough information for those decisions without requiring callers to infer the business
   outcome from a bare boolean, Active Record state, or error-message text. A record can be a named
   payload; the operation's result owns the outcome contract.
4. Share a feature result only when operations have the same payload and outcome meanings. Keep
   common success/failure mechanics in the shared base and feature-specific policy with the feature.
   Add result fields for an actual caller requirement, not hypothetical future consumers.

Feature results used by endpoints own `http_status`; controllers retain template/body selection.
Keep Rails request objects, rendering, and persistence out of results. A semantic code describes an
outcome independently of the user-facing message. Test each distinction through the public service
and the caller's decision using [verification](../ruby/verification.md).

When adopting, extending, or checking compatibility with Autodidact's `ApplicationService` and
`ApplicationResult`, read the [sample base contract](result-compatibility.md). That reference owns
its custom keywords, exception classes, payload readers, and Ruby `Data` behavior. Those mechanics
are not assumed for another result implementation. Preserve established helpers rather than adding a
result/monad dependency solely to restate the same contract.

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
