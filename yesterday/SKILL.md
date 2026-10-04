---
name: yesterday
description:
  Assemble an ephemeral standup update from yesterday's Linear work, meetings, and Slack activity.
disable-model-invocation: true
---

# Yesterday

Build a standup brief from the prior local workday. Linear is required and is the source of truth
for assigned issue work. Google Calendar, Granola, and Slack are optional evidence sources.

## Reporting Window

1. Read the machine's local date, weekday, and timezone.
2. Set the reporting date to the previous calendar day, except on Monday, when it is the preceding
   Friday. Use that date from local midnight through 23:59:59.
3. State the date and timezone before gathering evidence. The window is correct when it covers one
   local workday.

## Gather Evidence

1. Identify the authenticated Linear user.
2. Find issues assigned to that user with activity in the reporting window. For each issue, gather
   its identifier, title, status transitions, and every issue comment posted in the window,
   including comments by other people.
3. Query every issue assigned to the user in an in-development status (for example In Progress or In
   Review), regardless of recent activity. Review each issue's recent comments and updates to check
   that the status still looks accurate, and to surface activity that the movement-based query
   missed. Flag issues that appear stale or finished but still sit in development.
4. If Google Calendar tools are connected, list the user's events in the reporting window to
   establish which meetings actually happened and who attended. Google Calendar is the schedule of
   record.
5. If Granola MCP tools are connected, read the note summaries for meetings in the window that
   involved the user. Extract decisions, commitments, action items, and unresolved questions
   relevant to the user's work. Granola is the record for transcribed huddles.
6. If Slack MCP tools are connected, search the window for the user's work messages and read
   relevant thread replies. Include only context that clarifies progress, feedback, decisions, or
   blockers; do not turn the brief into a message log.
7. Note each source that was unavailable or returned no evidence. Do not infer a meeting, huddle
   outcome, or work item from missing data. The evidence is complete when every available source has
   either contributed relevant context or been accounted for.

## Brief And Interview

Present a compact factual brief grouped by Linear issue, with `IDENTIFIER: title`, status movement,
and relevant comment, meeting, or Slack context. Include in-development issues that had updates but
no status movement, and flag any in-development issue whose status appears stale. Deduplicate
evidence repeated across sources.

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

Treat answers as the user's authoritative account. The interview is complete when every material
ambiguity has an answer or is explicitly marked unresolved.

## Standup Update

Draft concise past-tense bullets about work completed or advanced yesterday. Include issue
identifiers and titles when applicable. Combine related ticket transitions into one outcome-oriented
bullet; do not narrate raw status changes or repeat source text.

Include a `Blockers` bullet only when there is a real blocker, risk, or unresolved dependency.
Include untracked work as ordinary bullets. Keep the result ephemeral: do not create, update, or
store anything in Linear, Slack, Granola, Google Calendar, files, or memory.

End by asking whether the user wants the bullets revised.
