# React performance and verification

## Resolve Vercel guidance

For rendering, data loading, subscriptions, or bundle changes, read installed
`vercel-react-best-practices` and the rule files matching the changed concern. If unavailable, use
[Vercel's public skill](https://github.com/vercel-labs/agent-skills/blob/main/skills/react-best-practices/SKILL.md)
and its sibling `rules/` directory. Record the installed version or fetched revision/access date.

Choose rules from the actual execution path:

- Async requests: `async-*`; establish dependencies before parallelizing work.
- Client imports and heavy browser features: `bundle-*` and relevant `rendering-*` rules.
- State subscriptions and effects: `rerender-*`; inspect the state owner before adding memoization.
- Server rendering and serialized props: `server-*`, through the [Next.js layer](../nextjs/data.md)
  when applicable.

Load `vercel-composition-patterns` only for its [composition triggers](composition.md). The skills
own their detailed examples; these standards own local decisions and applicability. Vercel's impact
labels guide investigation rather than assigning severity to every diff. The library shown in an
example is not an adoption requirement. If an external source is unavailable, apply the local rules
and report the specific expansion that could not be assessed.

Before adding memoization, a shared cache, or lazy loading, identify the costly render, request, or
dependency and the user path it affects. Preserve behavior and compare the relevant measurement when
claiming an improvement. Keep simple derived expressions direct.

## Verify behavior at its owner

Use the project's existing tools. Cover transformations with focused tests; exercise components
through user-visible interactions and accessible controls. Cover pending, empty, success, and
failure states when that path supports them. Test navigation, persistence, and authentication in an
integration/browser flow when those boundaries change. Private handler calls and render-count
assertions alone do not establish the interaction contract.

Run type, lint, and build checks required by the repository. When changing client imports or
server/client composition, verify the production build as well as development rendering. Keep
performance claims separate from correctness evidence and record checks that remain unrun.
