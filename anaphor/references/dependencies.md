# Skill composition

Install the Anaphor family together; sibling links are dependencies. Resolve them relative to the
installed skill directory. If a required skill is missing, name it and its role; keep the dependent
step incomplete instead of substituting an unacknowledged workflow. Installation is a separate
action.

## Required engineering disciplines

Locate and read **Matt Pocock's** installed `tdd` before implementation and `code-review` before
review. Check authorship and content when another library exposes the same name.
[Attribution](../ATTRIBUTION.md) pins the sources used to design this draft. Record the installed
source used for the run; surface a material policy change before importing it into an ongoing
implementation.

TDD owns test quality, confirmed seams, and its implementation loop. Carry the user's testing
decisions from the accepted spec into that loop. Existing confirmation remains valid; ask only for
missing or materially changed test boundaries. Keep refactoring in the subsequent review/fix stage,
as that discipline specifies.

Anaphor uses `code-review` with these explicit orchestration adaptations:

- Supply the accepted spec and original baseline directly. Tracker discovery is needed only to
  retrieve missing requirements; a complete supplied spec does not require tracker onboarding.
- Preserve its Standards and Spec axes and labelled smell heuristics. Add Anaphor's separate
  Principles subagent and triggered Execution/risk passes through `anaphor-review`.
- Use the host's available agent mechanism and inherited model. When parallel execution is
  unavailable, run the axes sequentially in fresh contexts. Disclose when fresh contexts are
  unavailable.

The accepted `to-spec` document is an input artifact. Anaphor does not invoke its product synthesis
or ticket-publication workflow again.

## Conditional references

Read only the discipline whose branch is reached:

- `codebase-design`: an interface, ownership boundary, or test seam needs design work. Its
  `DESIGN-IT-TWICE.md` informs Anaphor's comparison procedure.
- `diagnosing-bugs`: a defect's cause remains unresolved after reproduction and tracing the affected
  path.
- `domain-modeling`: implementation exposes conflicting domain terms or relationships. Product
  changes still require the user's decision.
- `prototype`: an implementation question needs a disposable experiment. Keep the accepted spec
  fixed and record the answer before returning to implementation.
- `vercel-react-best-practices`: React/Next.js code reaches the Principles review. Read applicable
  rule files under the [frontend profile](../../anaphor-review/references/principles/frontend.md).
- `web-design-guidelines`: browser interface behavior reaches the Principles review. Use its current
  source and preserve finding anchors while adding Anaphor's evidence fields.
- Emil's UI skills: user-facing presentation or interaction changes reach the
  [UI craft profile](../../anaphor-review/references/principles/ui-craft.md). That profile owns the
  specialist triggers; resolve only the skills it selects from the host's installed collection. They
  are optional user-supplied references, not dependencies installed by this project's lock.

The [Principles profiles](../../anaphor-review/references/principles/README.md) own local language
checks and primary-source fallbacks. They can grow with specific review questions without copying an
entire external skill. Their optional source loading is separate from required TDD/code-review
dependencies.

These optional references augment the task; their absence does not invent a new mandatory phase.
Read their instructions when used and identify conflicts rather than silently dropping
prerequisites. User-invoked workflows such as `to-tickets` remain architectural inspirations, not
nested commands.
