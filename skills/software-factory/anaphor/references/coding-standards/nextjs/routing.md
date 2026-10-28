# Route composition

Choose the owner by responsibility:

1. Framework route contract: keep params/search-param adaptation, metadata exports, navigation, and
   route-level access decisions in the appropriate Next.js entry file. Follow the installed
   version's async route APIs rather than copying a version-specific signature from a sample.
2. Screen structure: a named component arranges meaningful page sections and their loading/error
   boundaries. Keep sibling section implementations in separate navigable modules.
3. Section behavior: the section owns its component, local types, data access, hooks, and tests.
   Shared section data belongs at their common feature owner.
4. Cross-route feature: move the feature as a unit to `src/features/<feature>/` or the repository's
   equivalent. Promote UI or integrations further only for an actual shared contract.

An illustrative App Router shape:

```text
src/app/projects/[projectId]/
  page.tsx
  loading.tsx
  error.tsx
  _project/
    project-screen.tsx
    project-header/
      project-header.tsx
      queries.server.ts
      types.ts
    project-members/
      project-members.tsx
      queries.ts
      queries.server.ts
      mutations.ts
      types.ts
      project-members.test.tsx
```

Create only modules and route boundaries the behavior needs. In this example `queries.ts` might own
browser-safe TanStack Query options while `queries.server.ts` owns protected data access; they are
distinct responsibilities, not duplicate implementations. A section used only here stays
route-local. Small helpers and private props can stay with their component, following
[React colocation](../react/colocation.md).

Keep screens and sections server-rendered by default in App Router. Needing an interactive member
filter does not make the route, header, and entire screen client components. Give the filter its
client boundary and compose it with server-rendered sections. Preserve independent loading where one
section need not block another; [data rules](data.md) own fetch scheduling and cache policy.

Next.js permits several organizational strategies. The route/screen/section split is Anaphor's
chosen convention, informed by the user's navigation preference and
[Next.js project organization](https://nextjs.org/docs/app/getting-started/project-structure).
