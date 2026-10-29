# Scopes, read services, and query objects

Read before adding or changing a Rails read path. Choose its owners in this order:

1. **Model scope:** a small, reusable filter or ordering with a stable meaning for that model. Keep
   it chainable. Screen-specific combinations and optional-filter policy belong with their read
   operation rather than accumulating as model-wide API.
2. **Read service:** the application entry point for a read use case, such as
   `Library::ReadCatalog`. It owns actor/tenant scope, accepted filters, ordering, pagination,
   loading, and the named result callers need. A simple read can apply model scopes or Active Record
   directly inside this service; a separate query class is not required.
3. **Query object:** extract a cohesive domain query when combinations of filters, joins,
   aggregations, or reuse give it a separate responsibility. Name it for the domain selection, such
   as `Library::CatalogItemsQuery`. One join or one lookup alone does not require extraction.

Read services and query objects perform reads. Operations that write records or trigger external
work use a distinct mutation use case.

The read service remains the public use case when it delegates selection to a query object. The
query object owns query construction or a documented projection/aggregate, not HTTP status policy,
rendering, or the application's whole read workflow. It can be a plain Ruby object with one public
`.call`; it does not need `ApplicationService` inheritance or a result wrapper for an internal
relation. Keep service responsibilities under the [application boundary](service-boundary.md).

Use `app/services/<capability>/` for read use cases and the existing query-object location when one
exists; otherwise place query objects in `app/queries/<capability>/` with Zeitwerk-compatible names.
Keep small model scopes on their model. The directory expresses ownership, not a parallel repository
framework to generate for every model.

## Preserve the caller's authorized selection

The read service establishes the actor's permitted relation before applying user filters. Pass that
relation explicitly to an extracted query object. Preserve its restrictions through every branch,
join, and subquery; never restart from an unrestricted model merely because a filter is omitted.
Check permissions for associated rows when their visibility differs from the root record.

Define what omission and blank input mean for each optional filter. A skipped optional filter
preserves the incoming relation; a required actor or ownership precondition cannot become an
optional filter. Accept explicit supported keys, validate domain values in the read use case, and
bind query values. Map user-selected sort fields/directions to known expressions rather than
interpolating request strings into SQL.

Choose and document whether the query object returns a composable relation or executed data.
[Query execution](query-execution.md) owns materialization, aggregates, preloading, and the boundary
between services and presentation.

## Source and adaptation

Based on Thiago Araújo Silva's thoughtbot article,
[A Case for Query Objects in Rails](https://thoughtbot.com/blog/a-case-for-query-objects-in-rails).
Its domain-query encapsulation, optional-filter behavior, relation input, and raw-data alternatives
inform this reference. Relation extensions with `extending` are an implementation option when they
simplify actual composition; the article's custom scope DSL is not required.

The read-service boundary, directory convention, required authorized relation, and presentation
execution policy are Anaphor decisions. Apply existing repository contracts before this fallback;
query extraction does not authorize changing an established result or authorization API.
