# The application boundary

Read when adding or changing a Rails use case, a controller/job/task caller, or the operation's
public inputs. The service exposes one business operation that callers can understand without
rebuilding its workflow from persistence calls.

## Separate adapters from operations

1. Identify the business process and name its service for that operation in the domain. Inserting a
   database row is one implementation step; it is not necessarily the whole business process.
2. Keep HTTP requests/rendering in controllers, job serialization/retry scheduling in jobs, and task
   argument parsing in tasks. Pass explicit actor/context and business data into the use case. Scope
   authorization inside the operation wherever a caller could otherwise bypass it.
3. Reuse the same operation from each adapter that needs the same business contract. A job or task
   must not reconstruct validation, authorization, transaction sequencing, or outcome decisions from
   a controller. Distinct operation promises still receive distinct services.
4. Trace all decisions and effects using the [Ruby service rules](../ruby/services.md). Keep Rails
   integrations concrete or injectable according to that reference's collaborator decision
   procedure.

**Boundary check:** follow each affected controller, job, or task to its public operation. When
several adapters need the same contract, verify that business sequencing has one owner and each
adapter supplies context and interprets the result. Inspect existing callers or a concrete accepted
caller scenario rather than adding unused adapters to demonstrate reuse. Verify caller outcomes
using the [public-boundary checks](../ruby/verification.md).

## Retained conventions and tradeoffs

_Sustainable Rails_, chapter 15, supplied for this change, informs this boundary and its emphasis on
visible behavior. Anaphor retains two deliberate differences:

- **Invocation:** the operation name lives in the service class; `.call` provides a common entry
  protocol and a fresh instance per invocation. Inputs stored during construction can sit farther
  from their use than method arguments. Keep them explicit and trace their use; retain private
  helper reuse within the operation. The chapter favors operation-named instance methods receiving
  the data directly. That alternative is not adopted by this update.
- **Results:** retain the existing shared service/result infrastructure while defining business
  outcomes for each operation. The chapter favors individually defined result classes. Shared
  mechanics can stay common; unrelated payloads and outcome policies remain feature-owned under
  [results and failures](results.md).

Keep per-invocation state on the fresh instance; shared singleton or class-level request state can
mix callers. Existing public contracts govern compatibility. These conventions do not authorize a
migration of an existing library's entry points or result protocol.
