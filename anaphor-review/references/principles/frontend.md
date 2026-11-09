# Frontend

Read for changed browser UI, component behavior, styles, or rendering/data loading. Layer these
checks onto the owning language profile. Vercel supplies performance and interface guidance; its
React/Next.js rules apply only when the project uses those frameworks.

## React and Next.js

**Trigger:** React components, hooks, or Next.js rendering/data boundaries change.

Read the installed `vercel-react-best-practices` skill and the applicable rule files. If absent, use
the [official skill][react-skill] as reference material. Record the installed version or fetched
revision/access date. Select rules for the changed execution path instead of copying its compiled
guide into every reviewer brief.

Anaphor's local review questions:

- **Waterfalls:** draw the actual data dependencies. Report avoidable serial work only when the
  operations are independent and concurrency respects rate, resource, and transaction constraints.
- **Client/server boundaries:** trace which imports and serialized values reach the client. Identify
  avoidable payload or an exposed capability; check the project's framework version before proposing
  server-only APIs. Keep a reachable authorization defect in the Security pass.
- **State and effects:** identify the source of truth and trace a user interaction. Show a stale
  value, unnecessary synchronization, or costly subscription before recommending a different state
  boundary or memoization. Compiler/runtime behavior and measured cost affect applicability.

Vercel's rule severity is not automatic severity for this diff. State the affected request, user
interaction, or workload. Avoid importing a new data-fetching library just to match an example.

## Browser interfaces, including non-React apps

**Trigger:** markup, controls, focus, navigation, loading/error feedback, or responsive behavior
changes.

Read installed `web-design-guidelines`, following its instruction to fetch current Vercel
guidelines. If the skill is absent, consult the [official interface guidelines][interfaces]
directly. If the source is unavailable, apply these local checks and report any material uncovered
concern.

- Trace keyboard operation and focus through the changed interaction. Check accessible names and
  native control semantics at the point a user acts, not merely whether an attribute is present.
- Follow submission and navigation through pending, success, and failure states. Check that the user
  can recognize the outcome and recover without losing necessary input.
- Inspect affected responsive or motion states where the change can hide a control or obstruct its
  use. Request a browser check from the verifier when source inspection cannot establish the result.

When the referenced skill returns terse `file:line` findings, retain those anchors and add the
Principles evidence, consequence, and applicability fields. This is an explicit reporting
adaptation; it does not replace the skill's applicable checks or claim browser execution from code
inspection.

## Expansion boundaries

Use the installed skill as the authority for its detailed rule set. Add local triggers, application
examples, or counterexamples when repeated reviews reveal a gap. For Vue, Svelte, or another
framework, use its own primary guidance for framework-specific behavior; the generic interface
checks remain applicable. Follow the [profile extension procedure](README.md).

Primary sources and installed skill definitions checked 2026-10-04:

[react-skill]:
  https://github.com/vercel-labs/agent-skills/blob/main/skills/react-best-practices/SKILL.md
[interfaces]: https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md
