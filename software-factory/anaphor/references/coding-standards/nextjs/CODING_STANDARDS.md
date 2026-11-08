# Next.js coding standards

Use for Next.js code when the [selection procedure](../README.md) selects this fallback. Apply
[React](../react/CODING_STANDARDS.md) to components and
[TypeScript](../typescript/CODING_STANDARDS.md) to typed code; each owns its rules once.

## Route entry and screen composition

Treat `page.tsx` as a route entry point. It adapts framework params/search params, performs
route-level access or navigation decisions, and renders a named screen component. Keep feature
transformations, large JSX sections, query implementations, and mutation workflows with the feature
that owns them. A small page may compose its named sections directly; a screen wrapper earns its
place through meaningful composition, not forwarding props unchanged.

The screen composes named section components. Each section can own a directory of colocated types,
queries, mutations, hooks, and tests. Keep sections navigable through concrete imports rather than
putting the whole page's implementation in `page.tsx`, one large screen, or one large screen hook.
Use [route composition](routing.md) for ownership and an example directory tree.

## Load the affected rules

- **Pages, layouts, feature placement, route-owned UI:** [route composition](routing.md).
- **Fetching, mutations, authorization, caching, streaming, server/client imports:**
  [data and server boundaries](data.md), based on Vercel's React/Next.js guidance.
- **Component APIs, state, effects, tests:** the matching
  [React references](../react/CODING_STANDARDS.md).
- **Contracts, external data, schemas, assertions:** the matching
  [TypeScript references](../typescript/CODING_STANDARDS.md).

Inspect the installed Next.js/React versions and router before selecting APIs. The `page.tsx`
conventions here target App Router; preserve Pages Router entry points and use its matching
framework documentation for existing Pages Router code. A fallback does not authorize a router,
framework, fetching-library, or caching migration.

**Complete a change:** trace route entry to screen, section, data owner, and server/client boundary.
Run the repository's checks and affected real flows; inspect serialization, authorization, and cache
isolation when those concerns change.
