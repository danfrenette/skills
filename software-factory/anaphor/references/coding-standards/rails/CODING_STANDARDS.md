# Rails API coding standards

Use this entry when Anaphor selects the Rails fallback. These standards govern Rails application/API
code, services, facades, persistence, and their tests. The [selection procedure](../README.md) owns
precedence, compatibility, and adoption.

## Core responsibilities

Controllers and Jbuilder views own HTTP concerns. Mutation services own business sequencing,
transaction boundaries, and write outcomes. Read-only facades own read coordination and expose
completed data. Each use case owns its authorization scope. Active Record models own associations,
persistence constraints, and simple reusable scopes. Mutation policies and external writes belong in
services; read composition and read-only provider calls belong in facades, so persistence callbacks
do not hide workflow execution.

Each action invokes one fixed, named use case. Give distinct operations distinct resource routes and
standard REST actions; selecting a service from request keys moves business dispatch into HTTP.
Mutation services inherit directly from the application service base; read facades are plain Ruby
objects. Keep feature-specific policy with its use case or result, rather than adding feature base
classes for query or validation shortcuts.

Name supporting mutation services by capability under `app/services/`. They may use Active Record
directly; add a domain object when it owns a real concept, rather than mirroring each table or
adding a repository layer by default. Extract only a stable owner with a distinct contract; keep
small explicit duplication when sharing would introduce behavior flags or optional preconditions.

## Load the affected rules

Before editing or reviewing each affected boundary, read all matching references:

- **Controllers, routes, JSON views, request input:** [HTTP](http.md).
- **Mutation use cases, service adapters, public service inputs:**
  [application boundary](service-boundary.md).
- **Mutation services or their collaborators:** [Ruby services](../ruby/services.md) and
  [arguments and defaults](../ruby/arguments.md). Rails `call` methods use roughly five business
  steps with necessary control flow and rescue clauses; the Ruby-library bareword rule is not a
  Rails requirement.
- **Results, error handling, reporting:** [results and failures](results.md).
- **Read-only actions, page data, dashboards, replacing read services:** [facades](facades.md).
- **Model scopes, index filtering, domain queries:** [query ownership](queries.md).
- **Query execution, pagination/counts, association loading, rendering reads:**
  [execution boundary](query-execution.md).
- **Models, writes, transactions, concurrent invariants:** [persistence](persistence.md).
- **Providers, subprocesses, files, temporary resources:**
  [resource boundaries](../ruby/resources.md).
- **Tests or behavior changes:** [verification](../ruby/verification.md), including its Rails
  branch.

**Complete a change:** account for every changed responsibility and applicable reference. Run the
repository's actual checks at the affected public boundaries; report uncovered contracts and
exceptions with their evidence. Read commands from project configuration and setup documentation
rather than treating this sample as an executable setup recipe.
