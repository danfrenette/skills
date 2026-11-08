# Composition and state

Before changing a component API, trace its callers and choose the source of variation:

- Different structure or workflow: compose named variants from shared pieces. Prefer children for
  structural slots. Keep render callbacks when the parent must supply item data or state.
- Shared state across sibling consumers: lift to their common owner; introduce a provider when
  context makes that capability available without passing it through unrelated intermediates.
- An ordinary state such as disabled or expanded: use a clear prop. The problem is combinations of
  workflow mode flags, not the boolean type itself.

Read installed `vercel-composition-patterns` for component API changes, then its matching rules:
`architecture-avoid-boolean-props`, `patterns-explicit-variants`,
`patterns-children-over-render-props`, or the relevant `state-*` rule. If unavailable, consult the
[public skill](https://github.com/vercel-labs/agent-skills/blob/main/skills/composition-patterns/SKILL.md)
and its sibling rules. Apply compound components only when they own a coherent shared contract.
Existing controlled/uncontrolled APIs and supported React versions constrain a refactor.

For state/effect changes, identify the source of truth before adding synchronization:

1. Computable from current props/state: derive during rendering.
2. Triggered by one interaction: run in its event handler or the owning mutation callback.
3. Synchronizes an external system: use an effect with complete dependencies and matching cleanup.
4. Holds server-owned data: use the existing query/cache owner instead of copying it into local
   state. A deliberate editable draft has its own reset/save contract.

Keep components at module scope; defining them inside renders can replace their identity and reset
state. Extract hooks by coherent behavior, not to hide an entire screen's unrelated responsibilities
behind one large hook. Verify sibling consumers see the same state after edits and remounts.

For state/effect details, load the matching `rerender-*` rules in `vercel-react-best-practices`
using [source resolution](performance.md). React's
[effect guidance](https://react.dev/learn/you-might-not-need-an-effect) explains the ownership test.
Use version-specific React APIs only when the project's installed version supports them.
