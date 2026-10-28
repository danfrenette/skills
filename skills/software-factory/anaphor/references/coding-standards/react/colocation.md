# Colocation and navigation

Choose a file's owner before choosing its directory:

1. Used by one component: keep it in that component's directory. Put extracted props and related
   types in a neighboring `types.ts`; a tiny props type can stay in the component file. Keep hooks,
   queries, mutations, schemas, pure transformations, fixtures, and tests nearby as they are needed.
2. Used by several components in one feature: keep it at their narrowest feature owner. A feature
   `types.ts` owns shared feature contracts, not every descendant's private props.
3. Used across features: promote the coherent capability and its tests to a shared owner. Share
   types from the module that defines the contract rather than moving them to a global types file.
4. Generated or external contracts: import from their generator/package owner or expose a deliberate
   boundary adapter. Keep generated output separate from handwritten component types.

Use concrete filenames such as `queries.ts`, `mutations.ts`, `filters.ts`, or `use-selection.ts`.
Keep unrelated behavior out of a catch-all `utils.ts`. Import concrete modules directly; broad
barrels hide dependencies and can pull server code into a client graph. Public package entry points
remain deliberate API contracts rather than incidental feature barrels.

A section directory may look like this; create only files that have a responsibility:

```text
project-members/
  project-members.tsx
  types.ts
  queries.ts
  mutations.ts
  use-member-filter.ts
  member-row.tsx
  project-members.test.tsx
```

Keep a small `member-row.tsx` beside its section. Give it its own directory when it acquires local
types, queries, or another cohesive implementation. This preserves click-through navigation without
requiring a folder or file for every declaration.

Use the existing query library. With TanStack Query, colocate feature query keys/options, query
functions, and mutation/invalidation behavior with the component or feature that owns the data. Keep
generic transport clients at their shared integration owner. A query hook is not a reason to create
one application-wide file of feature queries or to install TanStack into a project without it.
Framework-specific hydration and server ownership follow the [Next.js data rules](../nextjs/data.md)
only when Next.js is involved.

The navigation test: starting from screen JSX, a reader can follow a named import to its section and
find that section's contracts and data work nearby. If a change requires visiting unrelated global
files, reconsider ownership before adding another export there.

This folder policy is an Anaphor convention requested by the user, informed by Kent C. Dodds's
[colocation principle](https://kentcdodds.com/blog/colocation). It is not a folder prescription from
Vercel or Next.js.
