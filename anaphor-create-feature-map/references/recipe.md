# Feature recipe

Use an existing map's structure when it carries these facts. Keep reusable launch/doctor/cleanup
instructions in the local verification guide and link them from entries.

Each feature entry contains:

- **Outcome:** actor, starting state, action, expected visible or public result, and relevant
  durable effect. Link the accepted requirement when available.
- **Entry points:** real routes, commands, or public interfaces; name alternate paths and roles that
  change the outcome.
- **Prerequisites:** required target, identity/role, data, and setup pointers. Store credential
  retrieval instructions, never credentials.
- **Drive:** exact observed actions using stable labels, selectors, arguments, or requests.
  Reference an existing behavior test rather than duplicating its implementation.
- **Assertions:** success, meaningful failure states, and how persisted effects are read back.
  Expected results come from requirements, not the current possibly broken output.
- **Evidence:** what to capture and where it survives cleanup. Keep per-run receipts separate from
  the durable procedure.
- **Cleanup and gotchas:** owned resources, reset procedure, known limitations, and external effects
  requiring isolation.

The local guide supplies:

1. **Launch:** documented command and readiness signal, with the identity of the process started by
   this run. A one-shot command or library test needs no persistent server.
2. **Doctor:** read-only confirmation of target revision/build, health, access, and required state.
3. **Drive:** chosen harness and how feature entries use it.
4. **Evidence:** artifact location and links to receipts, retaining failed attempts.
5. **Cleanup:** exact owned resources to stop/remove, preserving evidence.

Discover commands and selectors from the project; ship no unresolved placeholders or
machine-specific generated URLs. Prefer a pointer to maintained commands over a cached copy of
package configuration. Keep the feature index linked to every recipe and label known coverage gaps.
