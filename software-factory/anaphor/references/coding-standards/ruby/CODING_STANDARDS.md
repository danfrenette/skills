# Ruby library coding standards

Use this entry when Anaphor selects the Ruby-library fallback. The
[selection procedure](../README.md) owns precedence, compatibility, and adoption.

## Core responsibilities

Keep source wrappers, normalized content, operations, and provider adapters distinct. Wrappers
provide access, commands perform operations, and content objects describe normalized data. External
formats and process details stay at adapter boundaries. Follow the project's loader and capability
namespaces so naming and file placement preserve constant loading.

Before extracting an object, name the policy, resource, or collaborator contract it owns. Keep
private steps together when they have one owner; forwarding layers add navigation without reducing
caller obligations. Prefer explicit duplication when sharing requires unrelated behavior flags.

Preserve the library's existing public entry points, result shape, and exception policy. A Rails
base service, HTTP status policy, or reporting wrapper is not part of this Ruby-library default.

## Load the affected rules

- **Commands, services, collaborators, application comments:** [services](services.md). Business
  orchestration uses the Ruby-library branch; low-level value/protocol helpers keep their own shape.
- **Constructors, options, omission, defaults:** [arguments](arguments.md).
- **Providers, processes, files, temporary resources, failure propagation:**
  [resources](resources.md).
- **Tests, behavior changes, verification commands:** [verification](verification.md).

**Complete a change:** account for every changed responsibility and applicable reference. Run actual
project checks at the public boundary; report uncovered contracts and exceptions with evidence. Use
configuration and setup documentation for commands and supported runtimes.
