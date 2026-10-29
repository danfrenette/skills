# Query execution and presentation

Read when changing where a query is built, executed, paginated, counted, or rendered. Assign the
execution owner before returning a value across a layer boundary.

## Keep lazy composition inside the application layer

- **Model scopes and relation-returning query objects** compose an `ActiveRecord::Relation`.
  Document that contract and let the read service finish its selection before loading records.
- **Data-returning query objects** may execute a documented aggregate or projection for the read
  service. Return a stable data shape and test it; callers cannot chain more relation operations
  onto that result. Keep the relation and data forms explicit rather than switching return types
  through a mode flag.
- **Read services** own final execution, directly or through a data-returning query object. Return
  named records, arrays, projections, and computed pagination/count data through the established
  result. Single-record finders execute within this boundary too. Preserve the service/result
  conventions in [results and failures](results.md).
- **Controllers, result objects, and views** consume that completed result. They do not construct
  queries, call terminal query operations, or trigger lazy association loading while rendering.

Returning a lazy relation inside a result only postpones work; it does not satisfy the execution
boundary. A loaded relation can still issue SQL if a consumer chains another query or calls a
querying method. Return the records or values needed by presentation and keep subsequent query
operations with the service.

## Finish the data shape before rendering

Apply authorized filters and deterministic ordering before limit/offset or the project's cursor
pagination. Include a stable tie-breaker when the primary sort is not unique. Compute required
totals from the intended authorized, filtered selection rather than accidentally counting only the
page or widening the scope. Use the repository's existing pagination mechanism.

Compose required association preloads before materialization. `joins` selects matching rows; it does
not by itself guarantee that later association access is loaded. Inspect every association the view
traverses, including nested collections. Loading the root array alone does not prevent later SQL.
Select all attributes the result contract needs; format the already-loaded data in Jbuilder.

Active Record builds relations lazily, while operations such as `to_a`/`load`, finders,
calculations, and `pluck` can execute queries depending on the operation and loaded state. A block,
enumeration, or association accessor can also trigger database work. Consult the installed Rails
version's [query guide](https://guides.rubyonrails.org/active_record_querying.html) and
[Relation API](https://api.rubyonrails.org/classes/ActiveRecord/Relation.html) when execution is
unclear.

## Verify the boundary

Use real database behavior to test the read operation's rows, cross-user/tenant exclusions, actual
filter combinations, ordering, pagination, and empty outcomes. Cover omitted optional filters
without dropping the authorized scope. For joins, check that returned records and required counts
retain their intended cardinality.

Load the service result, then observe SQL while the real view renders or the documented consumer
traverses its payload: this phase must issue no data queries. Use the repository's SQL
instrumentation or strict-loading support plus coverage for terminal operations; strict loading
alone does not catch every query a consumer could issue. Keep query-budget checks separate from
row-correctness assertions. Add bounded-query coverage when preloading or query fan-out changes;
avoid asserting private scope calls or incidental SQL text.

These execution and verification rules are Anaphor's application-boundary policy, not a claim that
thoughtbot's article mandates eager materialization. A deliberately streaming/exporting operation
needs its own documented batching, execution, and resource-lifetime contract rather than passing an
unbounded lazy relation to ordinary presentation code.
