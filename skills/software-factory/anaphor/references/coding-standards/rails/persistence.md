# Persistence and transactions

The coordinating use case owns authorization scope and transaction boundaries. Scope lookups to the
acting user before reading or changing owned resources. Supporting services can use Active Record;
controllers and result objects cannot own persistence work.

Models own associations, persistence constraints, and reusable simple scopes. Put business policies,
external calls, and workflow execution in services.

For each persisted invariant, distinguish user feedback from data integrity. Application validations
produce useful feedback; enforce invariants that the database can express with constraints such as
`NOT NULL`, foreign keys, unique constraints, and checks. Writers outside Rails, APIs that bypass
validations, and concurrent requests can evade application-only validation. Keep business policies
that depend on wider workflow context in the service rather than claiming every policy is a column
constraint. When an invariant or its enforcement changes, verify the constraint rejects an invalid
write that bypasses model validation; use the real database for that check.

Before a multi-step write, identify which effects must commit together. A returned failure does not
roll back an Active Record transaction: explicitly abort when a failed child invalidates earlier
writes. Test the persisted readback after failure, not only the returned result.

Keep network calls outside database transactions when the contract allows; rollback cannot undo an
external effect. Where atomicity is impossible, make partial effects and the caller's recovery
obligations explicit. Add retries or coordination only for an evidenced contract or reachable
failure, following Anaphor's robustness-scope procedure.
