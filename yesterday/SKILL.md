---
name: yesterday
description:
  Assemble an ephemeral standup update from yesterday's Linear work, meetings, messages, and agent
  sessions.
disable-model-invocation: true
---

# Yesterday

Build a standup brief from the prior local workday. Linear is required and is the source of truth
for assigned issue work. Every other source adds evidence when this machine and harness provide it.

## Reporting Window

1. Read the machine's local date, weekday, and timezone.
2. Set the reporting date to the previous calendar day, except on Monday, when it is the preceding
   Friday. Use that date from local midnight through 23:59:59.
3. State the date and timezone before gathering evidence. The window is correct when it covers one
   local workday.

## Gather Evidence

1. Take an inventory of the source directory below. Run each source's probe and record it as
   available, unavailable, or needing authorization.
2. If Linear is unavailable, stop and tell the user that the brief needs Linear.
3. For each available source, read its reference and follow it. Read references only for available
   sources.

The evidence is complete when every source is either gathered or recorded with its reason. Infer
meetings, outcomes, and work items only from evidence that exists.

### Source directory

- **Linear** (required): available when Linear MCP tools or the `linear` CLI exist. Read
  [Linear](references/linear.md).
- **Google Workspace**: available when Google Calendar or Gmail tools exist. Read
  [Google Workspace](references/google-workspace.md).
- **Granola**: available when Granola MCP tools exist. Read [Granola](references/granola.md).
- **Slack**: available when Slack MCP tools exist. Read [Slack](references/slack.md).
- **Agent sessions**: always read the [session router](references/sessions/README.md), with the
  reporting window as its session window. It probes each harness's local history.

A tool that exists but asks for authorization counts as needing authorization: name it in the brief
so the user can connect it.

## Brief And Interview

Open the brief with one orienting line: the reporting date, the sources read, and the headline (for
example, "Two issues moved; `ENG-123` waits on review"). Then present a compact factual brief
grouped by Linear issue, with `IDENTIFIER: title`, status movement, and relevant meeting, message,
or session context. Include in-development issues that had updates but no status movement, and flag
any in-development issue whose status appears stale. List evidence that maps to no issue under
`Untracked work`. Deduplicate evidence repeated across sources.

If no assigned Linear issue changed, say explicitly:

> No changes were recorded on issues assigned to you for [date]. This may mean your work was not
> reflected in Linear yet.

Ask these questions every run:

1. Were there blockers, risks, or unresolved dependencies to mention?
2. What did you do yesterday that these sources do not capture?

Then ask only questions needed to resolve ambiguity in the evidence. Useful examples include:

- A review comment appeared on `ENG-123`: did you address it or is follow-up still needed?
- `ENG-123` moved to review: what outcome or customer impact should the update mention?
- `ENG-123` is still in development but looks done or untouched: is the status still accurate, and
  should the update mention it?
- A meeting assigned you an action: did you complete it yesterday, or should it be framed as a
  follow-up?
- The session "Auth refactor" stopped mid-migration: should the update mention it as in progress?

Treat answers as the user's authoritative account. The interview is complete when every material
ambiguity has an answer or is explicitly marked unresolved.

## Standup Update

Draft concise past-tense bullets about work completed or advanced yesterday. Write each bullet for a
**cold reader**: a teammate at standup who knows the product but not the ticket. Use ASD-STE100
Simplified Technical English: active voice, one idea per bullet, at most 25 words. Include issue
identifiers and titles when applicable. Combine related ticket transitions into one outcome-oriented
bullet; do not narrate raw status changes or repeat source text.

Include a `Blockers` bullet only when there is a real blocker, risk, or unresolved dependency.
Include untracked work as ordinary bullets. Keep the result ephemeral: treat every source as
read-only, and keep the brief and bullets in this conversation.

End by asking whether the user wants the bullets revised.
