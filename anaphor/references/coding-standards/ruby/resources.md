# Results and resource boundaries

## Preserve failure contracts

Inspect the public dispatcher, result type, callers, and exception policy before editing a command.
A base may return failures or re-raise defects; a direct instance call may bypass its wrapper.
Preserve the established contract unless an API change is accepted. Inspect child results and stop
before dependent work; returning a failure does not halt the parent automatically.

Keep stage-specific errors useful without credentials or sensitive input content. An outage or
failed parse remains a failure rather than empty success. Normalize supported provider protocol
outcomes at adapters; add robustness for evidenced inputs and failures rather than hypothetical
in-process types.

## Own resource lifetimes

One owner acquires, uses, and releases each temporary resource. Keep cleanup in a block or `ensure`
covering success, process failure, and parsing. Return durable content or transfer explicit
ownership; a path whose temporary owner already released it is unusable.

Preserve original inputs: write outputs to distinct destinations. Use subprocess argument arrays
rather than interpolated shell strings. Isolate temporary resources across concurrent calls.
Document partial external effects because cleanup and database rollback cannot undo every effect.
