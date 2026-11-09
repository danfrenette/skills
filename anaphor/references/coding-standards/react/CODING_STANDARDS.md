# React coding standards

Use for React components, hooks, and their consumers when the [selection procedure](../README.md)
selects this fallback. Next.js adds its own layer; typed code also uses
[TypeScript](../typescript/CODING_STANDARDS.md).

## Core responsibilities

Compose screens from named components representing meaningful sections or interactions. Keep each
section's implementation, types, data access, transformations, and tests with its owning component
or feature. Follow [colocation](colocation.md) before adding or moving files; a global components,
hooks, or types file is not the default owner for feature-specific code.

Give each piece of state one owner. Keep state local until another consumer needs it, then lift it
to the narrowest shared owner. Compose child components through explicit props and children; add
context when consumers need a shared capability across that subtree. File extraction alone does not
make a component reusable or require a provider.

Use named, module-level components so readers can navigate from screen composition to a section's
implementation. A one-line wrapper earns extraction only through a meaningful responsibility or
contract. Keep small local helpers together when separating them would add navigation without
separating a responsibility.

## Load the affected rules

- **Components, feature folders, local/shared types, imports:** [colocation](colocation.md).
- **Props, variants, state, hooks, effects, component APIs:**
  [composition and state](composition.md).
- **Rendering cost, data loading, browser dependencies, tests:**
  [performance and verification](performance.md).
- **Next.js routes or server/client boundaries:** [Next.js](../nextjs/CODING_STANDARDS.md).
- **TypeScript props, state types, schemas, assertions:**
  [TypeScript](../typescript/CODING_STANDARDS.md).

**Complete a change:** trace each changed interaction through its state owner, component boundary,
and data dependency. Apply all triggered references, run the project's checks, and verify the
observable outcome. Preserve the project's design-system contracts and test harness.
