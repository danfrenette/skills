# Read-only facades

Read when implementing a read-only action, assembling data for a page, or replacing a read service.
A facade gives callers a small, domain-named interface to the data a read operation needs. It owns
coordination; presentation owns formatting and rendering.

## Choose the owner

1. **The operation changes state:** use a mutation service under the
   [application boundary](service-boundary.md). This includes business writes, deliveries, and job
   scheduling. Reads needed to decide or carry out that mutation stay inside the service.
2. **The operation only reads:** use a facade, including show pages, dashboards, reports, and index
   actions. It may combine models, read-only provider responses, and computed values behind named
   readers. Keep each facade focused on one read use case, rather than a feature-wide object with
   unrelated screens or mode flags.
3. **A filtered collection needs cohesive query logic:** delegate that selection to a
   [query object](queries.md). Long, filterable index lists are the usual case. A query object owns
   selection/projection, while the facade owns the read workflow and exposed data. Simple reads may
   use model scopes or Active Record directly; an index action alone does not require extraction.

The facade replaces the earlier read-service role. Keep existing repository entry points and result
contracts compatible when applying this fallback; changing an established API requires an explicit
migration decision. A new read-only facade does not inherit `ApplicationService` or require a shared
facade base.

## Load once, then expose data

Name the class for the read surface, such as `Library::CatalogFacade`, and place it under
`app/facades/<capability>/` unless the repository has an established facade location. Use a public
`.fetch` construction entry to validate domain inputs, establish actor/tenant permissions, compose
queries, order/paginate, preload associations, and materialize the data before returning. Require
actor/context inputs; a missing actor cannot silently select an unrestricted read.

Construct the returned facade from completed data. Its named readers and derived-value methods
operate on that data without database or network work. An in-memory total must state whether it
covers the page or the full filtered selection; obtain full-selection aggregates during loading.
Keep HTML, localized formatting, Rails request objects, and rendering in presentation.

Reuse the endpoint's [result and failure contract](results.md). If it requires a result wrapper,
return the loaded facade as a named payload and supply that payload on failures too. Expected
invalid filters, missing records, or provider unavailability have explicit outcomes. Preserve the
project's unexpected-error reporting/re-raise path without inheriting a mutation service just to
obtain its helpers. A plain facade return is appropriate only when the established caller contract
supports it.

Facade loading may read from multiple authorized sources. Keep each source's visibility rules and
failure meaning explicit; one permitted root does not authorize every associated record or provider
response. Writes such as cache refreshes belong to an explicit service or established infrastructure
policy, never a reader that silently changes application state. Follow
[query execution](query-execution.md) for loading, cardinality, and bounded-query checks.

When implementing or reviewing this split, read the [complete catalog example](query-example.md) for
a facade loading a filtered relation and returning named, completed data. Its `.fetch` builds the
facade; its readers are safe to use during rendering.

## Verify the read contract

Test the public facade entry with real database behavior for authorization, filters, empty data,
ordering, and pagination. Assert no application-data writes during loading. After it returns,
exercise every reader and required association under SQL instrumentation; this phase issues no data
queries. For providers, use controlled read-client fixtures and assert repeated reader access makes
no further calls. Keep mutation-service outcome and rollback tests at their own public boundary.

## Sources and adaptation

thoughtbot's [open-source page example][thoughtbot] combines several data sources in an object with
named readers and in-memory derived values, using `.fetch` as an alternate constructor. The [C2
Facade Pattern page][c2] is the linked conceptual background; its JavaScript-only content was not
available through the text reader.

Reserving services for mutations, assigning read authorization/loading to facades, and completing
I/O before presentation are Anaphor conventions. The article's cache-writing recovery strategy is
not adopted as an implicit facade responsibility.

[thoughtbot]: https://thoughtbot.com/blog/a-peek-behind-the-curtain-of-our-new-open-source-page
[c2]: https://wiki.c2.com/?FacadePattern
