# Attribution

Anaphor's architecture and instructions are informed by upstream skill collections, the engineering
sources below, and an earlier project-specific implementation workflow. This draft is an adaptation,
not an official distribution or endorsement of those sources.

## Lauren Tan's pstack

- Repository:
  [Cursor plugins / pstack](https://github.com/cursor/plugins/tree/e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a/pstack).
- Inspected version: **0.15.9**, revision `e43c7ee26e0038c6c1fa8380dd34ce86ff94cb2a`, on 2026-10-04.
- Influences: coordinator/playbook structure; bounded worker briefs and ownership; Arena-style
  comparisons; revision-bound verification; launch/doctor/drive/evidence/cleanup recipes;
  feature-map creation and live maintenance; evidence-backed PR explanations.
- Applicable license notice: [pstack MIT license](licenses/pstack-MIT.txt).

## Matt Pocock's skills

- Repository:
  [mattpocock/skills](https://github.com/mattpocock/skills/tree/24fe0ef7737efae15c87225755e9f6f5965e4888).
- Inspected revision: `24fe0ef7737efae15c87225755e9f6f5965e4888`, on 2026-10-04.
- Referenced disciplines: `tdd`, `code-review`, and conditionally `codebase-design`,
  `diagnosing-bugs`, `domain-modeling`, and `prototype`.
- Influences: accepted `to-spec` input; tracer-bullet slices; separate Standards and Spec axes;
  constraint-based design alternatives in `DESIGN-IT-TWICE.md`; contextual references and
  progressive disclosure from `writing-for-agents`.
- Applicable license notice: [Matt Pocock MIT license](licenses/matt-pocock-MIT.txt).

## Writing guidance

The draft was written using **Emil Kowalski's `emil-writing-skills`** as supplied for this work, and
Matt Pocock's **`writing-for-agents`**: concrete decision procedures, observable completion
criteria, reasons for non-obvious rules, and references disclosed at the branch that needs them.
These are authoring influences, not additional runtime dependencies.

## Language and framework review

The [Principles axis](../anaphor-review/references/principles/README.md) contains original Anaphor
review questions informed by thoughtbot's Ruby Science, Sandi Metz's writing, Kent C. Dodds's
testing guidance, Matt Pocock's Total TypeScript, and Vercel's React and interface guidelines. Each
profile links the specific primary sources and records its research date.

The Vercel skills are optional referenced sources, not bundled copies. Local profiles supply
triggers, evidence requirements, and applicability limits so the review can expand beyond a bare
skill invocation. Author heuristics remain distinct from mandatory repository rules.

UI craft review references selected official skills from
[Emil Kowalski](https://github.com/emilkowalski/skills) and
[Jakub Krehel](https://github.com/jakubkrehel/skills), installed through the project lock. The
[UI craft profile](../anaphor-review/references/principles/ui-craft.md) owns concern-specific
selection and read-only reporting adaptations. This replaces runtime references to the earlier
user-supplied Emil collection; its writing guidance remains an authoring influence.

Visual-design checks draw on Adam Wathan and Steve Schoger's public Refactoring UI material, linked
in its [conditional profile](../anaphor-review/references/principles/refactoring-ui.md). These
sources are guidance, not bundled copies or independent delivery approvals.

## Deliberate Anaphor choices

- Begin with an accepted spec; product discovery stays upstream.
- Keep environment provisioning in project-local procedures.
- Use one inherited model with distinct review questions and fresh contexts; agreement is not proof.
- Adopt Matt's TDD discipline, carrying forward already confirmed test boundaries.
- Adapt code-review's tracker discovery and parallel dispatch to supplied specs and host
  capabilities while preserving Standards/Spec separation.
- Add a separate Principles reviewer with expandable language/framework profiles and attributed
  sources. Keep Execution and specialized risk reviews distinct.
- Require affected feature-map updates and execution of every changed recipe.
- Create minimal affected-feature coverage when the map is absent.
- Separate product failure from unavailable verification prerequisites and documentation drift.
- Deliver draft PRs and durable Markdown walkthroughs; hosted Tours are optional.

Upstream research is pinned so the rationale is inspectable. Installed discipline versions may
differ: identify them when running and assess material differences explicitly. Future source updates
should be deliberate reviews, not silent replacements of these policies.

## Session continuation

Matt Pocock's [handoff](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff)
owns user-requested continuation documents. Inspected 2026-10-04 and installed through the project
lock. Its temporary document references existing artifacts; Anaphor retains draft-PR delivery and
the durable reviewer walkthrough as distinct outputs.
