# Arguments and defaults

For every proposed argument, inspect callers and accepted use cases, then choose in order:

1. No caller or accepted use case needs the choice: omit the argument. Test convenience alone does
   not justify expanding the public API.
2. Every caller must supply it: require it. Keep required preconditions explicit so omission cannot
   silently turn a guarded operation into an unguarded one.
3. Omission selects a normal value: use a concrete default or default expression. Replacing `nil`
   later invents an extra state without adding meaning.
4. Absence changes the operation: permit `nil` and document that meaning, such as omitting an
   optional provider flag.
5. Automatic discovery differs from an explicit override: represent that mode explicitly and test
   both paths. Resolve environment-dependent defaults during `call`, not construction.

For an existing argument, establish the behavior of omission, explicit `nil`, and explicit values
before editing. Preserve supported cases and test the changed boundary. A strict override stays
strict; a broken override must not silently select another installation. Add a sentinel or null
object only when those states must differ.

Count independent inputs even inside keyword hashes. A parsed request body may enter a Rails use
case as one transport payload only when the service immediately selects accepted fields and groups
cohesive data before business work. It is not a pass-through options bag for persistence. Split
operations with different promises into named contracts; introduce an input object only when its
related fields carry behavior or invariants.
