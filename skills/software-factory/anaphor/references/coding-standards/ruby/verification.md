# Verification

## Choose the public boundary

Test outcomes through public command/service `.call` or the owning source interface. Assert results
and observable effects rather than private helper order, so responsibility-preserving refactors do
not require rewriting behavior tests.

Select coverage from the changed risk:

- A prerequisite can fail: prove dependent work does not run.
- Files or processes are owned: prove cleanup and input preservation on success and failure,
  including parsing failure. Overlapping calls must retain isolated resources.
- A provider is involved: use controlled fixtures for ordinary tests and opt-in live checks for
  actual compatibility. Record fixture provenance and limits; a simulated process does not prove an
  installed runtime works.
- An operation gains a controller/job/task caller: test its business outcome through the common
  public service and the changed adapter's mapping. Keep framework retry or rendering policy in its
  adapter; shared business sequencing stays in the use case.
- Callers distinguish business outcomes: exercise each supported outcome and its required payload.
  At an adapter seam, prefer real result instances with verified service doubles when isolation is
  needed, so changed result requirements expose a stale caller contract.
- A base service/result API is introduced or changed: test compatibility at its public boundary,
  including supported omission/`nil` behavior, payload access, and wrapper semantics.
- Rails read selection or loading changes: apply the
  [query execution checks](../rails/query-execution.md) with a real database, including authorized
  filter combinations and data-query-free consumption after the service returns.
- Rails HTTP or writes change: request tests cover mapping, authentication, ownership, extra-field
  rejection, and expected failures. Use real database behavior for persistence and rollback after a
  failed child. Test nested report-once behavior, re-raising the original exception, and reporter
  failure when the application uses the reporting policy. For changed persisted invariants, follow
  the constraint checks in [persistence](../rails/persistence.md).

Reuse the repository's harness and run its required checks. RSpec is the source Rails convention; a
fallback alone does not authorize replacing an existing test framework. Keep live dependencies out
of default checks. A green suite demonstrates its asserted outcomes, not universal standards
compliance or real-provider compatibility.

## Place repeatable checks

Reuse an established command convention first. For a Ruby project choosing one, use named Rake tasks
for repeatable checks, with live checks under `verify:`. Keep task files limited to inputs and
dispatch; put assertions, fixture preparation, and cleanup in a focused verification harness under
`spec/verification/`. Use `bin/` for setup, console, or an intentional CLI. This gives agents one
discoverable check interface instead of parallel ad hoc script conventions.

Setup documentation owns binaries, models, credentials, runtime support, and readiness checks.
Verification recipes own actions, expected outcomes, cleanup, and evidence limits. Install through
explicit setup steps; a check reports missing dependencies instead of silently installing them.
Retain the tested source revision and distinguish readiness, controlled behavior, and live proof.

For documentation-only changes, check links and contracts, then walk the instructions through a
concrete task and inspect the resulting decisions. Runtime tests are required only for affected
runtime risks. Keep per-run evidence in the project's chosen temporary or external location.
