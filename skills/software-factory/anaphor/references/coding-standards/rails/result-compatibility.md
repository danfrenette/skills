# Autodidact service/result compatibility

Read only when adopting, extending, or verifying the Autodidact-style base described here. Inspect
its actual source and callers before relying on these mechanics; these are custom APIs, not Rails
built-ins. For another result mechanism, use the caller-oriented rules in
[results and failures](results.md) and preserve that mechanism's contract.

- `ApplicationResult` owns common `success`, `errors`, and `error_code` fields and status
  predicates. Define named business payloads with `ApplicationResult.define(:source)` or the
  operation's own payload name. Pass semantic failure codes using `error_code:`.
- Supply named payload keywords on success and failure, usually `nil` on failure. Read custom
  payload fields explicitly at serialization boundaries.
- In the original implementation, custom payload readers are not Ruby `Data` members. Inherited
  `to_h` and equality include the common fields but omit the named payload. Preserve the behavior
  with compatibility tests when changing the base; changing it requires an accepted contract change.
- `ApplicationService` owns common `NotFound` and `InvalidInput` exception types. Use cases own
  user-scoped lookups and required-value checks; feature exceptions name additional business
  failures.
- Implement and test the base API before building callers that assume it exists. The
  [failure/reporting policy](results.md) owns dispatch and exception handling; keep feature-specific
  HTTP status policy out of the common base.

This contract was adapted from the supplied Autodidact standards. It is an implementation option for
a new application adopting that base and a compatibility reference for its existing consumers. It is
not a requirement to replace a repository's established result implementation.
