# Rails API coding standards

Use this entry when Anaphor selects the Rails fallback. These standards govern Rails application/API
code, supporting services, persistence, and their tests. The [selection procedure](../README.md)
owns precedence, compatibility, and adoption.

## Core responsibilities

Controllers and Jbuilder views own HTTP concerns. Use-case services own authorization scope,
business sequencing, transaction boundaries, and results. Active Record models own associations,
persistence constraints, and simple reusable scopes. Business policies and external calls belong in
services so persistence callbacks do not hide workflow execution.

Each action invokes one fixed, named use case. Give distinct operations distinct resource routes and
standard REST actions; selecting a service from request keys moves business dispatch into HTTP. Use
cases inherit directly from the application service base. Keep feature-specific policy with its use
case or result, rather than adding feature base classes for query or validation shortcuts.

Name supporting services by capability under `app/services/`. They may use Active Record directly;
add a domain object when it owns a real concept, rather than mirroring each table or adding a
repository layer by default. Extract only a stable owner with a distinct contract; keep small
explicit duplication when sharing would introduce behavior flags or optional preconditions.

## Load the affected rules

Before editing or reviewing each affected boundary, read all matching references:

- **Controllers, routes, JSON views, request input:** [HTTP](http.md).
- **Services or collaborators:** [Ruby services](../ruby/services.md) and
  [arguments and defaults](../ruby/arguments.md). Rails `call` methods use roughly five business
  steps with necessary control flow and rescue clauses; the Ruby-library bareword rule is not a
  Rails requirement.
- **Results, error handling, reporting:** [results and failures](results.md).
- **Models, writes, transactions, concurrent invariants:** [persistence](persistence.md).
- **Providers, subprocesses, files, temporary resources:**
  [resource boundaries](../ruby/resources.md).
- **Tests or behavior changes:** [verification](../ruby/verification.md), including its Rails
  branch.

**Complete a change:** account for every changed responsibility and applicable reference. Run the
repository's actual checks at the affected public boundaries; report uncovered contracts and
exceptions with their evidence. Read commands from project configuration and setup documentation
rather than treating this sample as an executable setup recipe.
