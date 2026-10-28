# Persistence and transactions

The coordinating use case owns authorization scope and transaction boundaries. Scope lookups to the
acting user before reading or changing owned resources. Supporting services can use Active Record;
controllers and result objects cannot own persistence work.

Models own associations, persistence constraints, and reusable simple scopes. Put business policies,
external calls, and workflow execution in services. Enforce invariants with database constraints
when concurrent writers can bypass application-only checks.

Before a multi-step write, identify which effects must commit together. A returned failure does not
roll back an Active Record transaction: explicitly abort when a failed child invalidates earlier
writes. Test the persisted readback after failure, not only the returned result.

Keep network calls outside database transactions when the contract allows; rollback cannot undo an
external effect. Where atomicity is impossible, make partial effects and the caller's recovery
obligations explicit. Add retries or coordination only for an evidenced contract or reachable
failure, following Anaphor's robustness-scope procedure.
