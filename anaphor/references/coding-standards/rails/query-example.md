# Relation extension example

Read when implementing or reviewing the [required relation-query convention](queries.md). Keep the
extension module, query class, and facade in separate Zeitwerk-compatible files.

This example assumes `user.catalog_items` is the complete authorized selection and each item's owner
is visible under the same policy. If associated rows have separate visibility rules, the facade
supplies those restrictions too. The adapter supplies string-or-nil filters and an integer page; the
facade validates domain values and normalizes blank optional filters to `nil`. Use the project's
established result and pagination APIs; the example assumes the
[`ApplicationResult.define` contract](result-compatibility.md).

## Filter module: `app/queries/library/catalog_item_filters.rb`

```ruby
module Library
  module CatalogItemFilters
    def with_status(status)
      return self if status.nil?

      where(catalog_items: { status: status })
    end

    def with_owner_name(name)
      return self if name.nil?

      joins(:owner).where(owners: { name: name })
    end
  end
end
```

Both filters narrow the current relation. The join adds a condition without replacing the caller's
selection. If a filter uses a subquery, derive it from the supplied permitted relation or a
separately authorized associated relation and retain the root selection. Resetting with `unscoped`,
rebuilding from an unrestricted model, or removing authorization predicates would break this
contract.

## Query class: `app/queries/library/catalog_items_query.rb`

```ruby
module Library
  class CatalogItemsQuery
    def initialize(scope:, status:, owner_name:)
      @scope = scope
      @status = status
      @owner_name = owner_name
    end

    def call
      @scope
        .extending(CatalogItemFilters)
        .select(:id, :owner_id, :title, :status)
        .with_status(@status)
        .with_owner_name(@owner_name)
    end
  end
end
```

The projection includes the owner foreign key required for preloading. The query returns a lazy
relation; neither the projection nor the domain filters load records.

## Facade: `app/facades/library/catalog_facade.rb`

```ruby
module Library
  class CatalogFacade
    Result = ApplicationResult.define(:catalog)
    PAGE_SIZE = 25

    def self.fetch(user:, status: nil, owner_name: nil, page: 1)
      status = status.presence
      owner_name = owner_name.presence
      unless (status.nil? || %w[draft published].include?(status)) && page.positive?
        return Result.new(
          success: false, catalog: nil,
          errors: ["Invalid catalog filters"], error_code: :invalid_input
        )
      end

      scope = user.catalog_items
      query = CatalogItemsQuery.new(scope: scope, status: status, owner_name: owner_name).call
      items = query.order(:id)
        .offset((page - 1) * PAGE_SIZE)
        .limit(PAGE_SIZE)
        .preload(:owner)
        .to_a
      Result.new(success: true, catalog: new(items: items))
    end

    attr_reader :items

    def initialize(items:)
      @items = items
    end

    def published_count_on_page
      items.count { |item| item.status == "published" }
    end
  end
end
```

The adapter invokes `Library::CatalogFacade.fetch(user: current_user, status: "published", page: 1)`
with validated transport types. The facade applies the authorization policy before delegation, then
orders, paginates, preloads, and materializes. This example retains a named result wrapper; keep the
project's feature-specific endpoint status and unexpected-error reporting policy around this entry.
Presentation reads `result.catalog.items`, loaded owners, and `published_count_on_page` without SQL.
See [facades](facades.md) for the read-only contract and [query execution](query-execution.md) for
count, cardinality, and SQL-boundary checks.
