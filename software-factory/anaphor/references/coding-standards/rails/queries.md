# Scopes, facades, and query objects

Read before adding or changing a Rails read path. Choose its owners in this order:

1. **Model scope:** a small, reusable filter or ordering with a stable meaning for that model. Keep
   it chainable. Screen-specific combinations and optional-filter policy belong with their read
   operation rather than accumulating as model-wide API.
2. **Facade:** the application entry point for a read-only use case, such as
   `Library::CatalogFacade`. It owns actor/tenant scope, accepted filters, ordering, pagination,
   loading, and the named data callers need. A simple read can apply model scopes or Active Record
   directly inside this facade; a separate query class is not required.
3. **Query object:** usually useful behind index actions with long, filterable lists. Extract a
   cohesive domain query when combinations of filters, joins, aggregations, or reuse give it a
   separate responsibility. Name it for the domain selection, such as `Library::CatalogItemsQuery`.
   One join or one lookup alone does not require extraction.

Facades and query objects perform reads. Operations that mutate application state or trigger
external writes belong to services. A mutation service may perform the reads needed by its workflow;
it does not need a facade for each lookup.

The facade remains the public read use case when it delegates selection to a query object. The query
object owns query construction or a documented projection/aggregate, not HTTP status policy,
rendering, or the application's whole read workflow. It can be a plain Ruby object with one public
`.call`; it does not need `ApplicationService` inheritance or a result wrapper for an internal
relation. Read [facades](facades.md) for the read interface and
[the application boundary](service-boundary.md) for mutation services.

Use `app/facades/<capability>/` for read facades unless the repository has an established location.
Use the existing query-object location when one exists; otherwise place query objects and their
extension modules in `app/queries/<capability>/` with Zeitwerk-compatible names. Keep small model
scopes on their model. The directory expresses ownership, not a parallel repository framework to
generate for every model.

## Preserve the caller's authorized selection

The facade establishes the actor's permitted relation before applying user filters. Pass that
relation explicitly to an extracted query object. Preserve its restrictions through every branch,
join, and subquery; never restart from an unrestricted model merely because a filter is omitted.
Check permissions for associated rows when their visibility differs from the root record.

Define what omission and blank input mean for each optional filter. A skipped optional filter
preserves the incoming relation; a required actor or ownership precondition cannot become an
optional filter. Accept explicit supported keys, validate domain values in the facade, and bind
query values. Map user-selected sort fields/directions to known expressions rather than
interpolating request strings into SQL.

## Require relation extensions for composable queries

Choose and document the return contract before implementing the query object:

- **Relation-returning query:** use Active Record `extending` with a separate, named module. This is
  required for every relation-returning query object. Put domain filters in that module's own file;
  each method operates on the current relation and returns an `ActiveRecord::Relation`. An omitted
  optional filter returns `self`, so skipping it preserves every existing restriction. The explicit
  relation interface keeps filters composable without adding screen-specific methods to the model.
- **Aggregate or data-returning query:** return the documented count, array, projection, or other
  data shape. Relation extension is not required when the query executes directly to produce data.
  Preserve the supplied authorization scope in that execution. A relation-returning helper used by
  the aggregate still follows the relation-extension convention.

The relation-returning query class extends its required authorized input relation, assembles the
projection, and composes the module's filter methods. Keep domain filter implementations in the
module and keep it independent of request state or facade instance variables. Relation construction
stays lazy: the module and query class return relations without enumerating, calculating, or loading
records. The facade retains authorization, input validation and normalization, ordering, pagination,
preloading, and materialization. Keep separate relation and data contracts rather than switching
between them through a mode flag.

When implementing or reviewing a relation-returning query, read the
[complete extension example](query-example.md) for the module, query class, and calling facade.
[Query execution](query-execution.md) defines the execution boundary and its verification.

## Source and adaptation

Based on Thiago Araújo Silva's thoughtbot article,
[A Case for Query Objects in Rails](https://thoughtbot.com/blog/a-case-for-query-objects-in-rails).
Its domain-query encapsulation, optional-filter behavior, relation input, and raw-data alternatives
inform this reference. Active Record documents the chainable extension interface in
[`QueryMethods#extending`](https://api.rubyonrails.org/classes/ActiveRecord/QueryMethods.html#method-i-extending).
Use a named module directly; the article's custom scope DSL is not required.

Requiring relation extensions, the facade/service boundary, directory convention, required
authorized relation, and presentation execution policy are Anaphor decisions. Apply existing
repository contracts before this fallback; query extraction does not authorize changing an
established result or authorization API.
