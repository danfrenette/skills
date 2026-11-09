# Agent handoffs

Use the host's actual subagent and worktree capabilities. Inherit its selected model by default; a
provider roster is not a prerequisite. Separate questions and contexts provide perspectives, while
executable evidence establishes behavior.

Before dispatch, give each worker:

- Role and the decision or change it owns.
- Accepted criteria and confirmed test boundaries.
- Working paths, baseline/revision, and applicable project instructions.
- For implementation, the project's readiness evidence and ownership of the supplied environment.
- Scope of permitted writes and shared resources it must leave to their owner.
- For implementation and review, [robustness scope](robustness-scope.md) and existing user decisions
  on hardening, so delegation preserves the authorized complexity budget.
- Relevant source references, feature recipes, and verification expectations.
- Required return: changes or findings, revision, commands/actions actually run, evidence locations,
  and unresolved gaps.

Before dispatch, save the spec, research notes, exploration findings, and evidence as files the
worker can read. Link them, and name the sections each change needs, instead of copying their
contents into every message or asking the worker to gather them again. Keep the assigned role, write
boundaries, and completion requirements explicit in the handoff, and confirm each worker can access
the referenced artifacts.

Disable conversation-history inheritance so reviewers assess source before the builder's defense.
With Codex's `collaboration.spawn_agent`, set `fork_turns: "none"` explicitly; on other hosts, use
the corresponding supported isolation option. A new agent identifier alone does not establish a
fresh context. Record the dispatch option used. If isolation is unavailable, disclose reduced
separation.

Give reviewers accepted requirements, pinned source, applicable standards, and verification
provenance. Keep the initial brief separate from the builder's design defense and other reviewers'
verdicts. After recording initial findings, reviewers may consult that rationale and explain any
resulting changes. Isolation removes inherited conversation, not access to relevant source or docs.
Reviewers can read files and run nonmutating checks; one verifier owns any shared app session or
mutable test data.

Each shared checkout, process, browser session, or data set has one writer. Parallel implementation
requires isolated resources and an integration owner. Keep dependent work sequential; a dependency
is complete only after its changes and evidence are accepted.

With limited concurrency, run roles sequentially in fresh contexts. With one context, perform named
passes and disclose the reduced separation. Never describe role agreement as independent model
consensus.

The coordinator checks returned diffs and evidence. A worker's report arrives when its turn ends;
output from a job that outlives the turn never reaches the coordinator. A handoff missing its
revision or observed results is incomplete. Return it to the same worker with the missing items.

Route review fixes to a fresh implementation worker. Give it the findings, the change's diff, and
the brief; it becomes the implementation owner for those fixes. Resume an existing implementation
session only to finish work it left unfinished. Affected review and verification follow.
