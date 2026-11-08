# Data and server boundaries

For each changed data path, identify its caller, trust boundary, dependencies, lifetime, and
invalidation rule before selecting an API. Read the relevant Vercel rules through
[React source resolution](../react/performance.md); these checks adapt them to Next.js.

## Place execution and trust

Use Server Components for initial server data and composition; use Client Components for browser
APIs, event handlers, and interactive state. Put `use client` at the smallest boundary that owns
those capabilities. Protect server-only integrations with `import 'server-only'`; a `.server.ts`
suffix is a navigation convention, not an enforcement mechanism. Pass only necessary serializable
props across the boundary and keep credentials and server imports out of client graphs.

Authenticate and authorize inside each Server Action and route handler that accesses protected data
or mutates state. Scope reads and writes to the actor. Page/layout guards improve navigation but do
not protect independently callable operations. Validate external input before business work; the
[TypeScript boundary rules](../typescript/boundaries.md) own validation and transport contracts.

## Schedule data and retain isolation

Draw dependencies first. Start independent requests together when resource limits permit; await
prerequisites before dependent operations. Let async sections fetch independently when that avoids a
page-level waterfall. Place Suspense boundaries around content with an independent loading
experience; wrapping an already-awaited result does not enable streaming.

Select caching deliberately from the installed version's APIs. Private data stays request-scoped
unless an explicit isolation design defines identity keys, lifetime, and invalidation. Request
deduplication and cross-request caching have different lifetimes; never keep mutable request/user
state in shared module variables. Mutations update or invalidate the owning cache before presenting
freshness as established.

When TanStack Query already owns browser data, colocate query keys/options and mutation cache
updates with the section/feature. Scope server QueryClient instances to the request; hydrate through
the project's existing provider/boundary and serialize only allowed data. Decide whether server or
client owns freshness to avoid independent copies drifting. Use
[TanStack's server-rendering guidance](https://tanstack.com/query/latest/docs/framework/react/guides/advanced-ssr)
for that branch; keep its version matched to the project. Initial server rendering alone does not
require introducing a client query library.

## Source branches

- Fetch scheduling/streaming: Vercel `async-parallel`, `async-suspense-boundaries`, and
  `server-parallel-fetching`.
- Protected operations: `server-auth-actions` and the installed Next.js authentication guidance.
- Serialization/cache lifetime: `server-serialization`, `server-cache-react`, and applicable
  cache/isolation rules in the selected skill version. A shared-cache example does not establish
  user-data isolation for this application.
- Framework boundaries:
  [Next.js Server and Client Components](https://nextjs.org/docs/app/getting-started/server-and-client-components).

Keep these references conditional to the changed concern. A missing external expansion leaves a
named coverage limit; it is not permission to guess version-specific behavior.
